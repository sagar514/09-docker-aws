# Build the Frontend (need dist folder)
# Copy content of dist folder in Backend/public folder

FROM node:20-alpine AS frontend-builder

WORKDIR /app

COPY ./Frontend /app

RUN npm install

RUN npm run build

# Create the Backend 
FROM node:20-alpine

WORKDIR /app

COPY ./Backend /app

RUN npm install

COPY --from=frontend-builder /app/dist /app/public

CMD ["node", "server"]