#���ñ�����
CC=g++

#debug�ļ������makefile�ļ���Ҫ���ִ�У�����������Ҫִ�е���Ŀ¼Ҫ�ų�debug�ļ��У�����ʹ��awk�ų���debug�ļ��У���ȡʣ�µ��ļ���
SUBDIRS=$(shell ls -l | grep ^d | awk '{if($$9 != "debug" && $$9 != "lib" && $$9 != "doc" && $$9 != "boost") print $$9}')

#������һ�е�ע�ʹ��룬��Ϊ�����Ѿ�֪��debug���makefile�����ִ�еģ��������ֱ��ȥdebugĿ¼��ִ��ָ����makefile�ļ����У�����������ע��
#DEBUG=$(shell ls -l | grep ^d | awk '{if($$9 == "debug" && $$9 != "lib" && $$9 != "doc" && $$9 != "test") print $$9}')

#��ס��ǰ���̵ĸ�Ŀ¼·��
ROOT_DIR=$(shell pwd)

#����bin�ļ������֣����Ը���Ϊ�Լ���Ҫ��
BIN=launch

#Ŀ���ļ����ڵ�Ŀ¼
OBJS_DIR=debug/obj

#bin�ļ����ڵ�Ŀ¼
BIN_DIR=debug/bin

#��ȡ��ǰĿ¼�µ�c�ļ��������ڱ���CUR_SOURCE��
CUR_SOURCE := $(wildcard *.c) $(wildcard *.cc)

#����Ӧ��c�ļ���תΪo�ļ�����������CUR_OBJS������
CUR_OBJS := $(patsubst %.c, %.o, $(patsubst %.cc, %.o, $(CUR_SOURCE)))

#�����±�����������shell�У������൱�ڵ�������Ŀ¼�µ�makefile��
export CC BIN OBJS_DIR BIN_DIR ROOT_DIR

#���ӿ����(�ڶ�̬��ǰ����-WI,-Bdynamic �ھ�̬��ǰ����-WI,-Bstatic)
LDFLAGS := -L./lib -WI,-Bdynamic -lstdc++ -lpthread -WI,-Bstatic -rdynamic

#C�������
CFLAGS := -Wall -DOPENSSL_THREADS  -D_THREAD_SAFE -D_THREADSAFE -D_REENTRANT -D_GNU_SOURCE -g -fPIC 

#CPP�������
CPPFLAGS := -Wall -g -Wl,--no-as-needed -rdynamic -ldl

#ע�������˳����Ҫ��ִ��SUBDIRS��������DEBUG
all:$(SUBDIRS) $(CUR_OBJS) DEBUG

#�ݹ�ִ����Ŀ¼�µ�makefile�ļ������ǵݹ�ִ�еĹؼ�
$(SUBDIRS):ECHO
	make -C $@
	
DEBUG:ECHO
	make -C debug	#ֱ��ȥdebugĿ¼��ִ��makefile�ļ�
	
ECHO:
	@echo $(SUBDIRS)
	
#��c�ļ�����Ϊo�ļ���������ָ������Ŀ���ļ���Ŀ¼�м�OBJS_DIR
$(CUR_OBJS):%.o:%.cc
	$(CC) -c $(CFLAGS) $(CPPFLAGS) $^ -o $(ROOT_DIR)/$(OBJS_DIR)/$@
	
clean:
	@rm -rf $(OBJS_DIR)/*.o
#@rm -rf $(BIN_DIR)/*