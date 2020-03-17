# gitlab-ci-ndk-android
This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool like GitLab CI. Make sure your CI environment's caching works as expected, this greatly improves the build time, especially if you use multiple build jobs. Thanks to https://www.github.com/sandrios/gitlab-ci-ndk-android and https://github.com/jangrewe/gitlab-ci-android.

A `.gitlab-ci.yml` with caching of your project's dependencies would look like this:

```
image: ahmadchoirunnajib/gitlab-ci-ndk-android

stages:
- build

before_script:
- export GRADLE_USER_HOME=$(pwd)/.gradle
- chmod +x ./gradlew

cache:
  key: ${CI_PROJECT_ID}
  paths:
  - .gradle/

build:
  stage: build
  script:
  - ./gradlew assembleDebug
  artifacts:
    paths:
    - app/build/outputs/apk/app-debug.apk
```
