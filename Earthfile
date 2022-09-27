VERSION 0.6
FROM zmkfirmware/zmk-build-arm:2.4

build:
  WORKDIR /opt

  COPY config/west.yml config/west.yml

  RUN west init -l config && \
      west update && \
      west zephyr-export

  COPY config/boards config/boards
  COPY config/*.keymap config/*.dtsi config/

  RUN --mount=type=cache,target=/root/.cache/zephyr --mount=type=cache,target=/opt/build/left \
    west build -s zmk/app -d build/left -b adv360_left -- -DZMK_CONFIG="/opt/config" && \
    mv /opt/build/left/zephyr/zmk.uf2 /opt/left.uf2

  SAVE ARTIFACT /opt/left.uf2 AS LOCAL left.uf2
  
  RUN --mount=type=cache,target=/root/.cache/zephyr --mount=type=cache,target=/opt/build/right \
    west build -s zmk/app -d build/right -b adv360_right -- -DZMK_CONFIG="/opt/config" && \
    mv /opt/build/right/zephyr/zmk.uf2 /opt/right.uf2

  SAVE ARTIFACT /opt/right.uf2 AS LOCAL right.uf2
