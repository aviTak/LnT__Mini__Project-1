# Name of the project
PROJECT_NAME = Student
TEST_PROJ_NAME = Test_$(PROJECT_NAME)
# All source code files
SRC = src/delete.c src/display.c \
src/insert.c src/main.c src/search.c src/update.c \

# Output Files
BUILD = build

# All test source files

TEST_SRC = src/delete.c src/display.c \
src/insert.c src/search.c src/update.c \
test/student_test.c \
unity/unity.c\

ifdef OS
   RM = del /q
   FixPath = $(subst /,\,$1)
   EXEC = exe
else
   ifeq ($(shell uname), Linux)
      RM = rm -rf
      FixPath = $1
	  EXEC = out
   endif
endif


TEST_OUTPUT = $(BUILD)/Test_$(PROJECT_NAME).$(EXEC)

# All include folders with header files
INC	= -Iinc\
-Iunity

#Library Inlcudes
#if working with CUnit 
#INCLUDE_LIBS = -lcunit

#INCLUDE_LIBS =

# Project Output name
PROJECT_OUTPUT = $(PROJECT_NAME).$(EXEC)

# Document files
DOCUMENTATION_OUTPUT = documentation/html

# Default target built
$(PROJECT_NAME):all

# Run the target even if the matching name exists
.PHONY: run clean test doc all

all: $(SRC) $(BUILD)
	gcc $(call FixPath,$(SRC)) $(INC) -o $(call FixPath,$(BUILD)/$(PROJECT_NAME).$(EXEC))

# Call `make run` to run the application
run: all
	$(call FixPath,$(BUILD)/$(PROJECT_NAME).$(EXEC))

# Document the code using Doxygen
doc:
	make -C ./documentation

# Build and run the unit tests

test:$(BUILD)
	gcc  $(call FixPath,$(TEST_SRC)) $(INC) -o $(call FixPath,$(BUILD)/$(TEST_PROJ_NAME).$(EXEC))
	./$(call FixPath,$(BUILD)/$(TEST_PROJ_NAME).$(EXEC))

#Coverage
coverageCheck:$(BUILD)
	g++ -fprofile-arcs -ftest-coverage -fPIC -O0 $(TEST_SRC) $(INC) -o $(call FixPath,$(BUILD)/$(TEST_PROJ_NAME).$(EXEC))
	./$(TEST_OUTPUT)

# Create new build folder if not present
$(BUILD):
	mkdir build

# Remove all the built files, invoke by `make clean`
clean:
	$(RM) $(call FixPath,$(BUILD)/*)
	rmdir $(BUILD)