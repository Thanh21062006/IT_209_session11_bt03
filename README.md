# Báo cáo Thực hành DevOps - Session 11: Bài 3

## Tối ưu tốc độ CI bằng Gradle Dependency Caching

### 1. Giới thiệu tổng quan
Bài thực hành tập trung vào kỹ thuật tối ưu hóa hiệu năng và thời gian thực thi của luồng CI trong GitHub Actions. Bằng cách bổ sung thuộc tính `cache: 'gradle'` vào action `actions/setup-java@v5`, hệ thống sẽ tự động lưu vết và tái sử dụng toàn bộ các dependencies, plugins và Gradle wrapper đã tải từ các kho lưu trữ từ xa (Maven Central), loại bỏ việc tải lại trùng lặp ở các lần chạy tiếp theo.

### 2. Cấu trúc thư mục bài nộp
```text
SS11_HW03_DaoTrongTri_PTIT062/
├── .github/
│   └── workflows/
│       └── ci.yml             # Kịch bản CI kích hoạt tính năng cache: 'gradle'
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── src/
│   ├── main/
│   │   ├── java/com/ptit/devops_ss11/Application.java
│   │   └── resources/application.properties
│   └── test/
│       └── java/com/ptit/devops_ss11/ApplicationTests.java
├── .gitignore
├── build.gradle
├── gradlew
├── gradlew.bat
├── settings.gradle
├── README.md                  # Hướng dẫn tổng quan
└── REPORT.md                  # Báo cáo kỹ thuật so sánh benchmark thời gian CI trước/sau khi cache
```

### 3. Cấu hình Caching cốt lõi
```yaml
      - name: Thiết lập môi trường Java JDK 17
        uses: actions/setup-java@v5
        with:
          java-version: '17'
          distribution: 'temurin'
          cache: 'gradle'
```

Chi tiết phân tích cơ chế tạo cache key, dữ liệu đo đạc thực tế giữa lần chạy 1 và lần chạy 2 vui lòng xem tại [REPORT.md](REPORT.md).
