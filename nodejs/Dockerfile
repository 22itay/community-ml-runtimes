# ###########################################################################
#
#  CLOUDERA COMMUNITY RUNTIMES
#
# (C) Cloudera, Inc. 2025
#  All rights reserved.
# 
#  Applicable Open Source License: Apache 2.0 
#
#  NOTE: Cloudera open source products are modular software products 
#  made up of hundreds of individual components, each of which was 
#  individually copyrighted.  Each Cloudera open source product is a 
#  collective work under U.S. Copyright Law. Your license to use the 
#  collective work is as provided in your written agreement with  
#  Cloudera.  Used apart from the collective work, this file is 
#  licensed for your use pursuant to the open source license 
#  identified above.
#
#  This code is provided to you pursuant a written agreement with
#  (i) Cloudera, Inc. or (ii) a third-party authorized to distribute 
#  this code. If you do not have a written agreement with Cloudera nor 
#  with an authorized and properly licensed third party, you do not 
#  have any rights to access nor to use this code.
#
#  Absent a written agreement with Cloudera, Inc. (“Cloudera”) to the
#  contrary, A) CLOUDERA PROVIDES THIS CODE TO YOU WITHOUT WARRANTIES OF ANY 
#  KIND; (B) CLOUDERA DISCLAIMS ANY AND ALL EXPRESS AND IMPLIED 
#  WARRANTIES WITH RESPECT TO THIS CODE, INCLUDING BUT NOT LIMITED TO 
#  IMPLIED WARRANTIES OF TITLE, NON-INFRINGEMENT, MERCHANTABILITY AND 
#  FITNESS FOR A PARTICULAR PURPOSE; (C) CLOUDERA IS NOT LIABLE TO YOU, 
#  AND WILL NOT DEFEND, INDEMNIFY, NOR HOLD YOU HARMLESS FOR ANY CLAIMS 
#  ARISING FROM OR RELATED TO THE CODE; AND (D)WITH RESPECT TO YOUR EXERCISE 
#  OF ANY RIGHTS GRANTED TO YOU FOR THE CODE, CLOUDERA IS NOT LIABLE FOR ANY
#  DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, PUNITIVE OR
#  CONSEQUENTIAL DAMAGES INCLUDING, BUT NOT LIMITED TO, DAMAGES 
#  RELATED TO LOST REVENUE, LOST PROFITS, LOSS OF INCOME, LOSS OF 
#  BUSINESS ADVANTAGE OR UNAVAILABILITY, OR LOSS OR CORRUPTION OF
#  DATA.
#
#
############################################################################

## you can find updated version at 
## https://archive.cloudera.com/ml-runtimes/latest/artifacts/repo-assembly.json
ARG ML_RUNTIME_BASE_VERSION=2025.01.3-b8
ARG ML_RUNTIME_WORKBENCH_TYPE=python3.10-standard
ARG NODEJS_VERSION=22


# Start with a Base CML Runtime & upgrade
# Note: This particular image will use the Python base image
FROM docker.repository.cloudera.com/cloudera/cdsw/ml-runtime-pbj-workbench-${ML_RUNTIME_WORKBENCH_TYPE}:${ML_RUNTIME_BASE_VERSION}

RUN apt update && apt upgrade -y && apt clean && rm -rf /var/lib/apt/lists/*

ARG ML_RUNTIME_BASE_VERSION
ARG ML_RUNTIME_WORKBENCH_TYPE
ARG NODEJS_VERSION

# Install NODEJS by nvm
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV BASH_ENV=/home/cdsw/.bash_env \
    NVM_DIR=/home/cdsw/.nvm
VOLUME  /home/cdsw/.nvm
RUN touch "${BASH_ENV}" && echo '. "${BASH_ENV}"' >> ~/.bashrc && mkdir -p $NVM_DIR

RUN wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | PROFILE="${BASH_ENV}" bash
RUN nvm install ${NODEJS_VERSION} && nvm use ${NODEJS_VERSION}


RUN python -m pip install uv 


# Override Runtime label and environment variables metadata
ENV ML_RUNTIME_EDITOR="PBJ Workbench" \
    ML_RUNTIME_EDITION="Standard-node" \
    ML_RUNTIME_SHORT_VERSION="${ML_RUNTIME_SHORT_VERSION}" \
    ML_RUNTIME_DESCRIPTION="This runtime includes nodejs ${NODEJS_VERSION} and is based on PBJ Workbench image with ${ML_RUNTIME_WORKBENCH_TYPE} base on ${ML_RUNTIME_FULL_VERSION}" \
    ML_RUNTIME_MAINTENANCE_VERSION="1"

LABEL com.cloudera.ml.runtime.editor=$ML_RUNTIME_EDITOR \
      com.cloudera.ml.runtime.edition=$ML_RUNTIME_EDITION \
      com.cloudera.ml.runtime.full-version="${ML_RUNTIME_SHORT_VERSION}.${ML_RUNTIME_MAINTENANCE_VERSION}" \
      com.cloudera.ml.runtime.short-version=$ML_RUNTIME_SHORT_VERSION \
      com.cloudera.ml.runtime.maintenance-version=$ML_RUNTIME_MAINTENANCE_VERSION \
      com.cloudera.ml.runtime.description=$ML_RUNTIME_DESCRIPTION