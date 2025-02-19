# ResourceSpace DAM 10.5 Setup in GitHub Codespaces

This repository contains the setup for ResourceSpace DAM 10.5 in GitHub Codespaces.

## Getting Started

### Prerequisites

- GitHub Codespaces
- Docker

### Setup

1. Open this repository in GitHub Codespaces.
2. The development container will be set up automatically, installing Subversion (SVN) and starting the necessary services (Apache and MySQL).

### Using Subversion

Once the setup is complete, you can use Subversion in the terminal within your Codespace. For example, to check out the ResourceSpace DAM 10.5 repository:

```bash
svn checkout <URL_OF_RESOURCE_SPACE_DAM_10.5_REPO>
```

Make sure to replace `<URL_OF_RESOURCE_SPACE_DAM_10.5_REPO>` with the actual URL of the Subversion repository you want to check out.

### Follow ResourceSpace Setup Instructions

After checking out the repository, follow the ResourceSpace setup instructions to complete the installation and configuration.

### Configure the Database

1. **Create a MySQL Database**:
   - Connect to your MySQL server and run the following command to create a new database:

   ```sql
   CREATE DATABASE resourcespace CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   ```

   ResourceSpace will automatically create database tables, indexes, and so on.

2. **Database Users**:
   - It is a good security practice to create dedicated users for ResourceSpace.

   **Read-write access level**:

   ```sql
   CREATE USER 'resourcespace_rw'@'localhost' IDENTIFIED BY 'your_rw_password';
   GRANT ALL PRIVILEGES ON resourcespace.* TO 'resourcespace_rw'@'localhost';
   ```

   **Read-only access level**:

   ```sql
   CREATE USER 'resourcespace_r'@'localhost' IDENTIFIED BY 'your_r_password';
   GRANT SELECT ON resourcespace.* TO 'resourcespace_r'@'localhost';
   ```

   **IMPORTANT**: Please make sure to change the passwords given as an example above.

3. **Update Database Configuration**:
   - Update the ResourceSpace configuration files with your database connection details.

### Configure PHP

1. **Update `php.ini` Settings**:
   - Increase memory limit, upload size, and time-out limit in the `php.ini` file.
   - You can find the `php.ini` file in the PHP installation directory.

2. **Install Required PHP Extensions**:
   - Ensure that the GD library and other required PHP extensions are installed.

### Set Permissions

1. **Make 'filestore' and 'include' folders writable**:
   - Run the following commands to set the appropriate permissions:

   ```bash
   chmod 777 filestore
   chmod -R 777 include
   ```

### Complete the Setup Process

1. **Access ResourceSpace in the Browser**:
   - Open the configured URL in your browser to start the setup process.
   - Provide the database connection details and create an administrator account.

2. **Run Installation Check**:
   - Go to `Admin -> System -> Installation Check` to ensure everything is configured correctly.

### Set Up Cron Job

1. **Set Up `cron_copy_hitcount.php`**:
   - Set up a cron job to run `cron_copy_hitcount.php` once each night.

### Enable Additional Features

1. **Install ImageMagick and FFmpeg**:
   - Install ImageMagick and FFmpeg to enable thumbnail previews for more image and video file formats.
   - Set the paths to the binaries in `config.php`.

2. **Disable Apache Indexes Option**:
   - Ensure that the Indexes option is not set in Apache to prevent the 'filestore' folder from being publicly available.