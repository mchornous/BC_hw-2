CXX        := -c++
CXXFLAGS   := -pedantic-errors -Wall -Wextra -Werror -fPIC
LDFLAGS    := -L/usr/lib -lstdc++ -lm
BUILD      := ./build
APPL_OBJ_DIR := $(BUILD)/appl_obj
OBJ_DIR    := $(BUILD)/objects
APP_DIR    := $(BUILD)/apps
LIB_DIR    := $(BUILD)/lib
TARGET     := useCalculator
LIB_NAME    = MyLibrary
INCLUDE    := -Iinclude/
APPL_SRC   := $(wildcard src/*.cpp)
SRC        := $(wildcard src/modules/*.cpp)

APPL_OBJECT := $(APPL_SRC:%.cpp=$(APPL_OBJ_DIR)/%.o)
OBJECTS := $(SRC:%.cpp=$(OBJ_DIR)/%.o)

all: build $(APP_DIR)/$(TARGET)

$(APPL_OBJ_DIR)/%.o: %.cpp
	@mkdir -p $(@D)
	$(CXX) $(CXXFLAGS) $(INCLUDE) -o $@ -c $<

$(OBJ_DIR)/%.o: %.cpp
	@mkdir -p $(@D)
	$(CXX) $(CXXFLAGS) $(INCLUDE) -o $@ -c $<

$(APP_DIR)/$(TARGET): $(APPL_OBJECT) | $(LIB_DIR)/lib$(LIB_NAME).so
	@mkdir -p $(@D)
	$(CXX) $(CXXFLAGS) $(INCLUDE) $(LDFLAGS) -o $(APP_DIR)/$(TARGET) $^

$(LIB_DIR)/lib$(LIB_NAME).so: $(OBJECTS)
	$(CXX) -shared -Wl,-soname,lib$(LIB_NAME).so -o $(LIB_DIR)/lib$(LIB_NAME).so $^

.PHONY: all build clean debug release

build:
	@mkdir -p $(APP_DIR)
	@mkdir -p $(APPL_OBJ_DIR)
	@mkdir -p $(LIB_DIR)
	@mkdir -p $(OBJ_DIR)

debug: CXXFLAGS += -DDEBUG -g
debug: all

release: CXXFLAGS += -O2
release: all

clean:
	-@rm -rvf $(OBJ_DIR)/*
	-@rm -rvf $(LIB_DIR)/*
	-@rm -rvf $(APPL_OBJ_DIR)/*
	-@rm -rvf $(APP_DIR)/*

