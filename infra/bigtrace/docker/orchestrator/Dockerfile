# Copyright (C) 2024 The Android Open Source Project
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM debian:12

RUN apt update && apt install -y git python3 curl build-essential
RUN  git clone --depth 1 https://github.com/google/perfetto/
WORKDIR /perfetto
RUN tools/install-build-deps --grpc
RUN tools/gn gen out/dist '--args=is_clang=true enable_perfetto_grpc=true'
RUN tools/ninja -C out/dist orchestrator_main

CMD [ \
"/perfetto/out/dist/orchestrator_main", \
"-l", "worker:5052", \
"-r", "dns:///", \
"-s", "0.0.0.0:5051" \
]