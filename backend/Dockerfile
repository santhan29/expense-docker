FROM node:20 AS builder
WORKDIR /opt/server 
COPY package.json .
COPY *.js .
RUN npm install 




FROM node:20.18.0-alpine3.20 
EXPOSE 8080  
ENV DB_HOST="mysql" 
RUN addgroup -S expense && adduser -S expense -G expense && \
    mkdir /opt/server && \
    chown -R expense:expense /opt/server 
WORKDIR /opt/server 
COPY --from=builder /opt/server /opt/server 
USER expense 
CMD ["node", "index.js"] 


#here we are using host network so we have to give local host instead of container name 
#when we ar eusing bridge network we have to give mysql container name instead of ip address 

#before best practices implemented
# FROM node:20 
# EXPOSE 8080 
# ENV DB_HOST="mysql"   
# RUN mkdir /opt/server
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install 
# CMD ["node", "index.js"]