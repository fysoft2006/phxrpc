
include ../phxrpc.mk

LIB_HTTP_OBJS = http/http_client.o http/http_client.o http/http_msg.o http/http_proto.o

LIB_NETWORK_OBJS = network/socket_stream_base.o network/uthread_runtime.o network/uthread_epoll.o \
		   network/socket_stream_block.o network/socket_stream_uthread.o \
		   network/uthread_context_util.o network/uthread_context_base.o \
		   network/uthread_context_system.o network/timer.o \

LIB_FILE_OBJS = file/log_utils.o file/file_utils.o file/opt_map.o file/config.o

LIB_RPC_OBJS = rpc/phxrpc.pb.o rpc/http_caller.o rpc/server_config.o rpc/client_config.o \
		   rpc/socket_stream_phxrpc.o rpc/uthread_caller.o rpc/client_monitor.o rpc/server_monitor.o \
		   rpc/monitor_factory.o rpc/hsha_server.o \

LIB_OBJS = $(LIB_RPC_OBJS) $(LIB_HTTP_OBJS) $(LIB_NETWORK_OBJS) $(LIB_FILE_OBJS) \

TARGETS = libphxrpc.a

all: $(TARGETS)

libphxrpc.a: $(LIB_OBJS)
	$(AR) $@ $^
	mkdir -p $(PHXRPC_ROOT)/lib; cp $@ $(PHXRPC_ROOT)/lib

rpc/phxrpc.pb.cc: rpc/phxrpc.pb.h

rpc/phxrpc.pb.h: rpc/phxrpc.proto
	cd ..; $(PROTOBUF_ROOT)/src/protoc -I$(PROTOBUF_ROOT)/src -I. --cpp_out=. phxrpc/$<;

clean:
	@( $(RM) $(TARGETS) $(TEST_TARGETS) )
	@( $(RM) *.o core.* $(LIB_OBJS) )
	@( cd rpc; $(RM) *.pb.* )
