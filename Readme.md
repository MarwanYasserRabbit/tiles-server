Use tileserver-gl to start the server

and --verbose for debugging

pm2 start npm --name tileserver -- run start

docker-compose logs -f
docker-compose down
docker-compose up -d