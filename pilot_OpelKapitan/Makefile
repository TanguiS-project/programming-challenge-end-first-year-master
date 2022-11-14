PILOT_NAME = OpelKapitan

SRC_PATH = ./src
INC_PATH = ./include
OBJ_PATH = ./obj
BIN_PATH = ../drivers
LIB_PATH = ./lib
DIJ_PATH = /dijkstra
DIRECT_PATH = /direction
TOOLS_PATH = /tools

CC = gcc
CFLAGS = -Wall -Wextra -ansi -pedantic -O3
CPPFLAGS = -I$(INC_PATH) -L$(LIB_PATH)
LDFLAGS = -lm

SANITIZE=off
ifeq ($(SANITIZE),on)
CFLAGS += -fsanitize=address
endif
ifeq ($(DEBUG),off)
CFLAGS += -D'DEBUG'
endif

OBJS =     

DIJKSTRA_OBJS = $(OBJ_PATH)/dijkstraAlgo.o \
			    $(OBJ_PATH)/dijkstraMatrix.o
				
DIRECTION_OBJS = $(OBJ_PATH)/pilotDirection.o $(OBJ_PATH)/follow_line.o $(OBJ_PATH)/actionModificator.o $(OBJ_PATH)/straightAction.o $(OBJ_PATH)/boostAction.o $(OBJ_PATH)/simpleAction.o

TOOLS_OBJS = $(OBJ_PATH)/matrix.o $(OBJ_PATH)/pathList.o $(OBJ_PATH)/list.o

OTHER_OBJS = $(OBJ_PATH)/main.o $(OBJ_PATH)/communicatorWithGDC.o $(OBJ_PATH)/pilotManagement.o $(OBJ_PATH)/graph.o

OBJS = $(OTHER_OBJS) $(DIJKSTRA_OBJS) $(DIRECTION_OBJS) $(TOOLS_OBJS) 

all: try obj install

install: $(BIN_PATH)/$(PILOT_NAME) 

try: install
	cd ../drivers

$(BIN_PATH)/$(PILOT_NAME): $(OBJS)
	$(CC) $(CPPFLAGS) $(CFLAGS) $^ -o $(BIN_PATH)/$(PILOT_NAME) $(LDFLAGS)

$(OBJ_PATH)/main.o : $(SRC_PATH)/main.c
	$(CC) $(CFLAGS) $(CPPFLAGS) $< -o $@ -c 

$(OBJ_PATH)/%.o : $(SRC_PATH)$(DIJ_PATH)/%.c $(INC_PATH)$(DIJ_PATH)/%.h
	$(CC) $(CFLAGS) $(CPPFLAGS) $< -o $@ -c 

$(OBJ_PATH)/%.o : $(SRC_PATH)$(DIRECT_PATH)/%.c $(INC_PATH)$(DIRECT_PATH)/%.h
	$(CC) $(CFLAGS) $(CPPFLAGS) $< -o $@ -c 

$(OBJ_PATH)/%.o : $(SRC_PATH)$(TOOLS_PATH)/%.c $(INC_PATH)$(TOOLS_PATH)/%.h
	$(CC) $(CFLAGS) $(CPPFLAGS) $< -o $@ -c 

$(OBJ_PATH)/%.o : $(SRC_PATH)/%.c $(INC_PATH)/%.h
	$(CC) $(CFLAGS) $(CPPFLAGS) $< -o $@ -c 

obj:
	mkdir $(OBJ_PATH)
clean:
	rm -f $(OBJ_PATH)/*.o
distclean: $(BIN_PATH)
	make clean
	rm -f $(BIN_PATH)/$(PILOT_NAME)