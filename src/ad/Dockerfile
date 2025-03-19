FROM eclipse-temurin:21-jdk AS builder

WORKDIR /app

COPY build.gradle gradlew* settings.gradle ./

COPY ./gradle ./gradle

RUN chmod +x ./gradlew

COPY . .

RUN ./gradlew installDist -PprotoSourceDir=/app/pb

FROM eclipse-temurin:21-jre AS release

WORKDIR /app

COPY --from=builder /app/build/install/opentelemetry-demo-ad/ ./

ENV AD_PORT 9090

ENV FEATURE_FLAG_GRPC_SERVICE_ADDR=featureflagservice:50053

ENTRYPOINT [ "/app/bin/Ad" ]
