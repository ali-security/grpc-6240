# Copyright 2015 gRPC authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM debian:bullseye

ENV PIP_INDEX_URL="https://eyJjeXRob24iOiAiMC4yOS4yMiJ9:2021-10-26@time-machines-pypi.sealsecurity.io/"
# Install clang-tidy 11
RUN apt-get update && apt-get install -y clang-tidy-11 jq git
ENV CLANG_TIDY=clang-tidy-11

ADD clang_tidy_all_the_things.sh /

# When running locally, we'll be impersonating the current user, so we need
# to make the script runnable by everyone.
RUN chmod a+rx /clang_tidy_all_the_things.sh

CMD ["echo 'Run with tools/distrib/clang_tidy_code.sh'"]
