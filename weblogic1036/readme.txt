#build the image
docker build -t krol/weblogic1036 .

#run the image
docker run --rm=true -it krol/weblogic1036 /bin/bash
