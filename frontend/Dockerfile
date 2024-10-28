 # 1 passo
 FROM node:18.17.0 as build-stage
 
 RUN mkdir /usr/app

 COPY . /usr/app

 WORKDIR /usr/app

 ENV REACT_APP_BACKEND_URL=http://backend:5000

 RUN yarn

 ENV PATH /usr/srr/app/node_modules/.bin:$PATH

 RUN npm run build

 #2 PASSO
 # Use a imagem base do Nginx
 FROM nginx:latest

 WORKDIR /usr/share/nginx/html

 RUN rm -rf ./*

 COPY ./build . 
 #COPY --from=build-stage /usr/app/build .
 
 # config default modificada
 COPY nginx.conf /etc/nginx/conf.d/default.conf

 #ENTRYPOINT ["nginx", "-g", "daemon off;"]
