### MERN Blog App Deployment Guide (Week 10)

This is the full deployment guide of steps taken by Yousef (SDA2017) for the Week 10 assignment. 
The goal was to deploy a MERN stack blog app with the following architecture:

- Frontend: React app hosted on Amazon S3
- Media Uploads: Handled by a second S3 bucket
- Backend: Node.js API hosted on AWS EC2
- Database: MongoDB Atlas



### 1. MongoDB Atlas Setup

- Created an M0 free-tier cluster.
- Added database and collection.
- Whitelisted all IPs: (0.0.0.0/0).
- Created a DB user.
- Copied connection URI and updated credentials.


### 2. Frontend Setup and Deployment

- Entered (client/) folder and ran:

    (bash
  npm install
  npm run build
  )


- Created a public S3 bucket: (sda2017-blogapp-frontend)
- Enabled static website hosting (index.html).
- Uploaded the built files from (dist/) (Vite).
- Added public-read bucket policy.
- Verified access at: (http://sda2017-blogapp-frontend.s3-website.eu-north-1.amazonaws.com)


### 3. Media Upload Bucket

- Created second bucket: (sda2017-blogapp-media)
- Configured permissions with IAM policy allowing (PutObject), (GetObject), etc.
- Used this bucket for image/media uploads.


### 4. Backend EC2 Deployment

- Launched Ubuntu EC2 instance with (Yousef.pem)
- Allowed ports 22, 80, 5000 in security group.
- SSH into EC2:

    (bash
  ssh -i "Yousef.pem" ubuntu@<my-ec2-dns> /// I should put my DNS public IPv4 but I delete everything before I write this text & its work in browser 
  )

- Installed Node.js and PM2:

     (bash
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
  source ~/.bashrc
  nvm install --lts
  npm install -g pm2
  )

- Cloned repo or uploaded code.
- Created (.env) file manually in PowerShell:

    (powershell
  echo "JWT_SECRET=..." >> .env
  echo "MONGO_URI=..." >> .env
  )

- Installed backend dependencies:

    (bash
  cd server/
  npm install
  npm run build  
  pm2 start index.js --name blog-api
  )



### 5. AWS CLI (Chekcs for my security)

   (powershell
aws configure
# Will show me access key, secret & region
)


Assignment completed by Yousef (SDA2017) for Week 10.