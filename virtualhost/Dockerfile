FROM nginx:alpine

# Clean up default configs
RUN rm /etc/nginx/conf.d/default.conf

# Copy our subdomain config
COPY nginx.conf /etc/nginx/conf.d/

EXPOSE 80