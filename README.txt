Magic Oud Store Android app starter
Owner: Mohammad Raees Rahmaniname: Build Magic Oud Store APK

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Extract ZIP
        run: |
          mkdir project
          unzip -q *.zip -d project

      - name: Find Android project
        run: |
          ROOT=$(find project -type f \( -name settings.gradle -o -name settings.gradle.kts \) -print -quit | xargs dirname)
          echo "PROJECT_ROOT=$ROOT" >> $GITHUB_ENV

      - name: Set up Java
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - name: Build APK
        working-directory: ${{ env.PROJECT_ROOT }}
        run: |
          chmod +x gradlew
          ./gradlew assembleDebug

      - name: Upload APK
        uses: actions/upload-artifact@v4
        with:
          name: Magic-Oud-Store-APK
          path: ${{ env.PROJECT_ROOT }}/app/build/outputs/apk/debug/*.apk
Price: 50 AED per piece
Payments: Cash on Delivery and e& money / Payment Request
Orders: WhatsApp
Social links: Facebook, YouTube, TikTok (Instagram can be added later)

This is an Android Studio project. To make an APK, open the folder in Android Studio and Build > Build APK(s).
A live card-payment gateway is intentionally not included.
