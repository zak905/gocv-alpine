FROM ghcr.io/zak905/gocv-alpine/4.10.0-buildstage-go1.22.4

LABEL maintainer="Denis Makogon. mail: lildee1991@gmail.com"

ENV PKG="libstdc++ \
         ca-certificates \
         wget \
         libjpeg-turbo \
         libpng \
         libwebp \
         libwebp-dev \
         tiff \
         jasper \
         libavc1394 \
         openblas \
         libgphoto2 \
         gstreamer \
         gst-plugins-base "

RUN apk update && \
    apk upgrade && \
    apk add --no-cache ${PKG} && \
    # The gblic v2.28-r0 doesn't have sgerrand.rsa.pub.
    # Downloading it from previous version.
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.35-r1/glibc-2.35-r1.apk && \
    apk add --no-cache glibc-2.35-r1.apk && \
    rm -fr /glibc-2.35-r1.apk && \
    rm -rf /var/cache/apk/* && \
    apk del wget

ENV PKG_CONFIG_PATH /usr/local/lib64/pkgconfig
ENV LD_LIBRARY_PATH /usr/local/lib64
ENV CGO_CPPFLAGS -I/usr/local/include
ENV CGO_CXXFLAGS "--std=c++1z"
ENV CGO_LDFLAGS "-L/usr/local/lib -lopencv_core -lopencv_face -lopencv_videoio -lopencv_imgproc -lopencv_highgui -lopencv_imgcodecs -lopencv_objdetect -lopencv_features2d -lopencv_video -lopencv_dnn -lopencv_xfeatures2d -lopencv_plot -lopencv_tracking"
