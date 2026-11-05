#!/bin/bash
cd /test
echo "Pulling latest code from S3..."
/usr/local/bin/aws s3 cp s3://sam-project-bucket-2026-xyz/index.html ./index.html
echo "Restarting web server..."
sudo fuser -k 80/tcp
nohup python3 -m http.server 80 > server.log 2>&1 &
echo "Deployment complete!"