include ../config.mk

CC=cc
CFLAGS=-I../src -I../lib -I. -I.. -Wall -ggdb -DDEBUG -DWITH_CLIENT
LDFLAGS=-nopie
OBJS=context.o database.o logging.o memory.o net.o raw_send.o raw_send_client.o read_handle.o read_handle_client.o util.o

.PHONY: all clean

all : fake_user msgsps_pub msgsps_sub 
#packet-gen qos

fake_user : fake_user.o
	#${CC} $^ -o $@ ../lib/libmosquitto.so.0 -nopie
	${CC} $^ -o $@ -lmosquitto -nopie

fake_user.o : fake_user.c
	${CC} $(CFLAGS) -c $< -o $@

msgsps_pub : msgsps_pub.o
	${CC} $^ -o $@ ../lib/libmosquitto.so.0 -nopie

msgsps_pub.o : msgsps_pub.c msgsps_common.h
	${CC} $(CFLAGS) -c $< -o $@

msgsps_sub : msgsps_sub.o
	${CC} $^ -o $@ ../lib/libmosquitto.so.0 -nopie

msgsps_sub.o : msgsps_sub.c msgsps_common.h
	${CC} $(CFLAGS) -c $< -o $@

packet-gen : packet-gen.o
	${CC} $^ -o $@ ../lib/libmosquitto.so.0 -nopie

packet-gen.o : packet-gen.c
	${CC} $(CFLAGS) -c $< -o $@

qos : qos.o
	${CC} $^ -o $@ ../lib/libmosquitto.so.0 -nopie

qos.o : qos.c
	${CC} $(CFLAGS) -c $< -o $@

random_client : random_client.o ${OBJS}
	${CC} $^ -o $@ ${LDFLAGS}

random_client.o : random_client.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

context.o : ../src/context.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

database.o : ../src/database.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

logging.o : ../src/logging.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

memory.o : ../src/memory.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

net.o : ../src/net.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

raw_send.o : ../src/raw_send.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

raw_send_client.o : ../src/raw_send_client.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

read_handle.o : ../src/read_handle.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

read_handle_client.o : ../src/read_handle_client.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

util.o : ../src/util.c ../src/mqtt3.h
	${CC} $(CFLAGS) -c $< -o $@

clean : 
	-rm -f *.o random_client qos msgsps_pub msgsps_sub fake_user test_client
