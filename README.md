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


import csv
import requests
from tika import parser

# Assuming the GeoGazetteer REST server is running at this URL
geo_gazetteer_url = 'http://localhost:8765'

# Function to get geographic data from text using Tika GeoTopicParser
def get_geodata(text):
    headers = {'Accept': 'application/json'}
    response = requests.post(geo_gazetteer_url, data=text, headers=headers)
    if response.status_code == 200:
        return response.json()
    return None

# Load your BFRO sightings data
with open('bfro_sightings.csv', 'r') as csvfile:
    reader = csv.DictReader(csvfile)
    sightings = [row for row in reader]

# Iterate through the sightings and enrich with location data
for sighting in sightings:
    text = sighting['sighting_description']  # need to change
    geo_data = get_geodata(text)
    sighting['location_name'] = geo_data['location_name'] if geo_data else None
    sighting['latitude'] = geo_data['latitude'] if geo_data else None
    sighting['longitude'] = geo_data['longitude'] if geo_data else None

# Save the enriched data back to a new CSV file
with open('bfro_sightings_enriched.csv', 'w', newline='') as csvfile:
    fieldnames = sightings[0].keys()
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(sightings)



在Linux系统中，$HOME环境变量通常代表当前用户的主目录，其通常是/home/username，其中username是您的用户名。如果您看到指示HOME lucene-geo-gazetteer src，这可能是在描述路径时的一个格式错误，它可能应该是$HOME/lucene-geo-gazetteer/src。如果确实如此，那么下面是您应该使用的命令：

从您的主目录开始，克隆lucene-geo-gazetteer仓库：
bash
Copy code
cd $HOME
git clone https://github.com/chrismattmann/lucene-geo-gazetteer.git
进入克隆的仓库目录：
bash
Copy code
cd $HOME/lucene-geo-gazetteer
运行Maven构建命令：
bash
Copy code
mvn install assembly:assembly
接下来，要将lucene-geo-gazetteer的bin目录添加到您的PATH环境变量中，确保您可以从任何地方运行其提供的脚本。为此，您需要编辑您的shell配置文件（取决于您使用的shell，比如.bashrc或.profile），然后将路径添加到PATH变量中。
如果您使用的是Bash shell，可以这样做：

bash
Copy code
echo 'export PATH=$PATH:$HOME/lucene-geo-gazetteer/src/main/bin' >> ~/.bashrc
source ~/.bashrc
确保您替换命令中的路径以匹配您的实际目录结构。以上命令会把lucene-geo-gazetteer的bin目录添加到PATH环境变量，并立即应用更改。如果您的shell不是Bash，您可能需要编辑不同的配置文件，比如.zshrc或.profile。
