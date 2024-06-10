docker build -t jenkins-pipeline .

docker run -p 80:8080 -p 50000:50000 jenkins-pipeline

# Save image
docker commit <container_id> <image_name>
docker save -o <output_file_name>.tar <image_name>
docker load -i <output_file_name>.tar