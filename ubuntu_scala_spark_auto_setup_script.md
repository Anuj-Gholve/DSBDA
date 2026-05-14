# Ubuntu Automatic Setup Script for Scala + Apache Spark

This script automatically installs:

- Java (OpenJDK 11)
- Scala
- Apache Spark
- Environment Variables

It also configures the PATH automatically.

---

## Step 1: Create the Script File

Open terminal and run:

```bash
nano setup.sh
```

Paste the following code inside the file:

```bash
#!/bin/bash

# Update system
sudo apt update -y

# Install Java
sudo apt install openjdk-11-jdk -y

# Install Scala
sudo apt install scala -y

# Install wget and tar
sudo apt install wget tar -y

# Go to home directory
cd ~

# Download Apache Spark automatically
wget https://downloads.apache.org/spark/spark-3.5.6/spark-3.5.6-bin-hadoop3.tgz

# Extract Spark
tar -xzf spark-3.5.6-bin-hadoop3.tgz

# Rename Spark folder
mv spark-3.5.6-bin-hadoop3 spark

# Add environment variables automatically
cat <<EOF >> ~/.bashrc

# JAVA
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export PATH=\$PATH:\$JAVA_HOME/bin

# SCALA
export SCALA_HOME=/usr/share/scala
export PATH=\$PATH:\$SCALA_HOME/bin

# SPARK
export SPARK_HOME=\$HOME/spark
export PATH=\$PATH:\$SPARK_HOME/bin:\$SPARK_HOME/sbin

EOF

# Reload environment variables
source ~/.bashrc

# Show installed versions
echo "================================="
echo "Installation Completed!"
echo "================================="

java -version
scala -version
```

---

## Step 2: Save the File

Press:

- CTRL + O
- Enter
- CTRL + X

---

## Step 3: Give Execution Permission

```bash
chmod +x setup.sh
```

---

## Step 4: Run the Script

```bash
./setup.sh
```

---

## Step 5: Verify Spark

Run:

```bash
spark-shell
```

If successful, you will see:

```scala
scala>
```

---

## Test Spark

Inside spark-shell:

```scala
val data = Seq(1,2,3,4,5)
val rdd = spark.sparkContext.parallelize(data)
rdd.collect()
```

Expected output:

```scala
Array[Int] = Array(1,2,3,4,5)
```

Exit using:

```scala
:quit
```

---

## Fun Fact

entity["software","Apache Spark","distributed data processing engine"] can process huge datasets in memory, making it much faster than traditional Hadoop MapReduce for many big-data tasks.

