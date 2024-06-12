FROM node:18-alpine

COPY / /
RUN npm install
RUN npm run build 
EXPOSE 3000
# HEALTHCHECK --interval=5s --timeout=2s --retries=30 \
#   CMD wget --no-verbose --tries=1 --spider http://0.0.0.0:3000/health || exit 1

CMD ["node", "/build/index.js"]