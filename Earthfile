VERSION 0.6
FROM zmkfirmware/zmk-build-arm:2.4

build:
  WORKDIR /opt

  COPY config/west.yml config/west.yml

  RUN west init -l config && \
      west update && \
      west zephyr-export

  COPY config config

  RUN --mount=type=cache,target=/root/.cache/zephyr west build -s zmk/app -d build/left -b adv360_left -- -DZMK_CONFIG="/opt/config"
  SAVE ARTIFACT build/left/zephyr/zmk.uf2 AS LOCAL left.uf2
  
  RUN --mount=type=cache,target=/root/.cache/zephyr west build -s zmk/app -d build/right -b adv360_right -- -DZMK_CONFIG="/opt/config"
  SAVE ARTIFACT build/right/zephyr/zmk.uf2 AS LOCAL right.uf2
