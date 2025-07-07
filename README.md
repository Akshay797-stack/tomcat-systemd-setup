# tomcat-systemd-setup

A simple, production-style setup to deploy a Java `.war` application using Apache Tomcat and `systemd` on a Linux server. This repository provides a sample `.war` file and a custom `tomcat.service` unit to manage Tomcat as a background service.

---

## 📂 Contents

- `tomcat.service` – Custom systemd service file to manage Tomcat.
- `sample.war` – Sample Java web application (can be replaced with your `.war` file).
- `README.md` – Setup and usage instructions.
- `LICENSE` – MIT License.

---

## ⚙️ Prerequisites

Ensure the following before proceeding:

- A Debian/Ubuntu-based Linux system (other distros also work with minor changes)
- Root or `sudo` privileges
- Java installed (`OpenJDK 11` or above recommended)
- Apache Tomcat (Tested on Tomcat 9+)

---

## 🛠 Installation Steps

### 1. Install Java (if not already installed)

```bash
sudo apt update
sudo apt install openjdk-21-jdk -y
java -version
```

### 2. Download and Set Up Apache Tomcat

  ```bash
    wget https://downloads.apache.org/tomcat/tomcat-10/v10.1.11/bin/apache-tomcat-10.1.11.tar.gz
    tar -xzf apache-tomcat-10.1.11.tar.gz
    sudo mv apache-tomcat-10.1.11 /opt/tomcat
    sudo chmod +x /opt/tomcat/bin/*.sh
  ```

### 3. Deploy Sample WAR Application

  ```bash
    sudo cp sample.war /opt/tomcat/webapps/
  ```

### 4. Configure systemd Service

  ```bash
   sudo cp tomcat.service /etc/systemd/system/
    sudo systemctl daemon-reexec
    sudo systemctl daemon-reload
    sudo systemctl enable tomcat
    sudo systemctl start tomcat
  ```

### 5.Verify Deployment

  Open your browser and go to:
      ```bash
      http://<your-server-ip>:8080/sample/
      ```
  Check service status:
       ```bash
       sudo systemctl status tomcat
       ```

### Notes
  Ensure port 8080 is open in your firewall.
  WAR files are automatically deployed to /opt/tomcat/webapps/.
  Logs are available at /opt/tomcat/logs/.

### Contributing
Contributions are welcome! Feel free to:

  Fork this repository
  Improve automation or add features
  Create pull requests with enhancements

## License

This project is licensed under the [MIT License](LICENSE)

---

Let me know if you'd like to:
- Add badges (e.g. build passing, license, etc.)
- Include instructions for auto-deploy with GitHub Actions
- Convert it into a shell-scripted auto-installer for easier reuse
