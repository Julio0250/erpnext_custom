FROM node:14-buster-slim

USER root
RUN mkdir /install_app
COPY install_app.sh /install_app
RUN cd /install_app
RUN chown root:root /install_app/install_app.sh
RUN chmod +x /install_app/install_app.sh


RUN apt-get update && apt-get install git -y 
RUN /install_app/./install_app.sh factura_electronica https://github.com/sihaysistema/factura_electronica_gt.git version-13

FROM frappe/erpnext-nginx:v13.7.0

COPY --from=0 /home/frappe/frappe-bench/sites/ /var/www/html/
COPY --from=0 /rsync /rsync
RUN echo -n "\factura_electronica" >> /var/www/html/apps.txt

VOLUME [ "/assets" ]

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
