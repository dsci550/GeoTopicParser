# GeoTopicParser
1. 更新软件包列表

打开终端并运行以下命令来更新您的软件包列表：

```bash
sudo apt update
```

 2. 安装Java

Lucene GeoGazetteer依赖于Java，因此您需要安装Java运行环境。可以使用以下命令安装Java：

```bash
sudo apt install default-jdk
```

3. 安装Git

Git用于克隆Lucene GeoGazetteer的代码仓库。可以通过以下命令安装Git：

```bash
sudo apt install git
```

4. 安装Maven

Maven是一个项目管理和构建工具，用于编译Lucene GeoGazetteer。使用以下命令安装Maven：

```bash
sudo apt install maven
```

5. 克隆Lucene GeoGazetteer仓库

现在您的系统已经安装了所有必需的软件，可以克隆Lucene GeoGazetteer的代码仓库了：

```bash
git clone https://github.com/chrismattmann/lucene-geo-gazetteer.git
cd lucene-geo-gazetteer
```

6. 使用Maven构建Lucene GeoGazetteer

在仓库目录中，运行以下命令来构建项目：

```bash
mvn install
```

7. 运行GeoGazetteer服务器

构建成功后，使用Java运行构建的JAR文件以启动服务器：

```bash
java -jar target/lucene-geo-gazetteer-*.jar
```

将`*`替换为实际的版本号。

 8. 验证服务器运行

在浏览器中访问`http://localhost:8765`或使用命令行工具（如curl）来检查服务器是否正在运行：

```bash
curl http://localhost:8765
```
