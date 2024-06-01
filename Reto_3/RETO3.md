version: '3.8'
services:
  teemii-frontend:
    image: dokkaner/teemii-frontend:latest
    ports:
      - "8080:80"
    networks:
      - teemii-network
    restart: always
    depends_on:
      teemii-backend:
        condition: "service_started"
  teemii-backend:
    image: dokkaner/teemii-backend:latest
    build:
      context: ./server
    networks:
      - teemii-network
    volumes:
      - teemii-data:/data
    environment:
      - EXPRESS_PORT=3000
      - SOCKET_IO_PORT=1555

volumes:
  teemii-data:
    name: "teemii-data"
networks:
  teemii-network:
    driver: bridge
