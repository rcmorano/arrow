# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.

FROM arrow:cpp

# install python specific packages
ARG PYTHON_VERSION=3.6
ADD ci/conda_env_python.yml /arrow/ci/
RUN conda install -c conda-forge \
        --file arrow/ci/conda_env_python.yml \
        python=$PYTHON_VERSION && \
    conda clean --all

ENV ARROW_PYTHON=ON

# build and test
CMD arrow/ci/docker_build_cpp.sh && \
    arrow/ci/docker_build_python.sh && \
    pytest -v --pyargs pyarrow
