#-----------------------------------------
#  IOTF 
#-----------------------------------------
IOTF_DIR = ../../iotf-embeddedc/lib
IOTF_NAME = libiotf.a

MQTT_SRC_DIR = ../../iotf-embeddedc/lib
#MQTT_SRC_FILES = $(wildcard $(MQTT_SRC_DIR)/*.c)
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTClient.c            
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTLinux.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTFormat.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTPacket.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTDeserializePublish.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTConnectClient.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTSubscribeClient.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTSerializePublish.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTConnectServer.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTSubscribeServer.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTUnsubscribeServer.c
MQTT_SRC_FILES += $(MQTT_SRC_DIR)/MQTTUnsubscribeClient.c

IOTF_SRC_DIR = ../../iotf-embeddedc
IOTF_SRC_FILES += $(IOTF_SRC_DIR)/iotfclient.c
IOTF_SRC_FILES += $(MQTT_SRC_FILES)

IOTF_OBJ_FILES = $(IOTF_SRC_FILES:.c=.o)
#OBJS = $(subst .c,.o,$(IOTF_SRC_FILES))

IOTF_INC_DIRS += -I ../../iotf-embeddedc
IOTF_INC_DIRS += -I ../../iotf-embeddedc/lib

# Make static lib
IOTF_COMPILER_FLAGS += -Wall 

IOTF_MAKE_CMD = $(AR) rcs $(IOTF_DIR)/$(IOTF_NAME) $(IOTF_OBJ_FILES)



#-----------------------------------------
#  DEMO 
#----------------------------------------
DEMO_DIR = ./bin
DEMO_NAME= ibm_demo

DEMO_SRC_DIR = ./src
DEMO_SRC_FILES += $(DEMO_SRC_DIR)/ibm_demo.c
DEMO_SRC_FILES += $(DEMO_SRC_DIR)/util.c
DEMO_SRC_FILES += $(DEMO_SRC_DIR)/sensor.cpp


DEMO_INC_DIRS = -I ./inc

DEMO_LIB_DIRS = -L $(IOTF_DIR) 

DEMO_LIBS += -ldl -lm -lupm-tsl2561 -lstdc++

DEMO_COMPILER_FLAGS += -g


DEMO_MAKE_CMD = $(CC) $(DEMO_INC_DIRS) $(IOTF_INC_DIRS) $(IOTF_SRC_FILES) $(DEMO_SRC_FILES) $(DEMO_COMPILER_FLAGS) $(DEMO_LIBS) -o $(DEMO_DIR)/$(DEMO_NAME) 


all: 
	ibm_demo


# $@ left side of the :
# $^ right side of the :
# $< first item in the dependency list

#$(ODIR)/%.o: $(SDIR)/%.cpp 
#    $(CC) -c $(INC) -o $@ $< 

#$(OUT): $(OBJS) 
#    ar rvs $(OUT) $^

#%.o: %.c Makefile
#	@$(CC) $(CFLAGS) -MMD -MP -c $< -o $@
#	$(CC) -c $(IOTF_INC_DIRS) -o $@ $< 

OBJ_DIR = ../iotf-embeddedc/

obj: 
	$(CC) -c $(IOTF_INC_DIRS) $(IOTF_SRC_FILES) -o $(OBJ_DIR)


iotf_lib: obj
	$(DEBUG)mkdir -p $(IOTF_DIR)
	$(DEBUG)$(IOTF_MAKE_CMD)

ibm_demo: 
	$(DEBUG)mkdir -p $(DEMO_DIR)
	$(DEBUG)$(DEMO_MAKE_CMD)

clean:
	rm -rf $(IOTF_DIR)/$(IOTF_LIB)
	rm -rf $(DEMO_DIR)/$(DEMO_NAME)

