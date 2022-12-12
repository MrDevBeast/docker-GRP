FROM golang

# if left blank app will run with dev settings
# to build production image run:
# $ docker build ./api --build-args app_env=production
ARG app_env
ENV APP_ENV $app_env

# it is okay to leave user/GoDoRP as long as you do not want to share code with other libraries
COPY . /go/src/github.com/user/GoDoRP/api
WORKDIR /go/src/github.com/user/GoDoRP/api

# added vendor services will need to be included here
RUN go mod init
RUN go get -u gorm.io/gorm
RUN go get "github.com/jinzhu/gorm/dialects/postgres"
RUN go get "time"

RUN go get "database/sql"
RUN go get "encoding/json"
RUN go get "fmt"
RUN go get "github.com/julienschmidt/httprouter"
RUN go get "log"
RUN go get "net/http"
RUN go get "os"
RUN go build

# if dev setting will use pilu/fresh for code reloading via docker-compose volume sharing with local machine
# if production setting will build binary
CMD if [ ${APP_ENV} = production ]; \
	then \
	api; \
	else \
	go install github.com/pilu/fresh && \
	fresh; \
	fi
	
EXPOSE 8080
