NON_METRIC_SPACE_LIBRARY=../../similarity_search/
NON_METRIC_SPACE_LIBRARY_INC=$(NON_METRIC_SPACE_LIBRARY)/include
NON_METRIC_SPACE_LIBRARY_LIB=$(NON_METRIC_SPACE_LIBRARY)/release

LIBS= -lthrift -lNonMetricSpaceLib -lboost_program_options

CXXFLAGS += -I$(NON_METRIC_SPACE_LIBRARY_INC)  -I./gen-thrift/
# Enable C++11
CXXFLAGS += -std=c++11
# OMP flags
CXXFLAGS += -fopenmp
# Debug flags
#CXXFLAGS += -g
#CXXFLAGS += -g -O3
CXXFLAGS += -O3

BIN=query_server query_client

all: $(BIN)

clean:
	rm -f *.o gen-thrift/*.o $(BIN)

THRIFT_SRC=$(wildcard gen-thrift/*.cpp)
THRIFT_OBJ=$(patsubst %.cpp,%.o,$(THRIFT_SRC))

# Note -pthread: this enables threads!!!
query_server:  $(THRIFT_OBJ) QueryService_server.o gen-thrift/*.h makefile $(NON_METRIC_SPACE_LIBRARY_LIB)/libNonMetricSpaceLib.a 
	$(CXX) -o$@  $(THRIFT_OBJ) QueryService_server.o -L/usr/local/lib -L$(NON_METRIC_SPACE_LIBRARY_LIB) $(LIBS) -pthread -fopenmp 

query_client:  $(THRIFT_OBJ) QueryClient.o gen-thrift/*.h makefile $(NON_METRIC_SPACE_LIBRARY_LIB)/libNonMetricSpaceLib.a 
	$(CXX) -o$@  $(THRIFT_OBJ) QueryClient.o -L/usr/local/lib -L$(NON_METRIC_SPACE_LIBRARY_LIB) $(LIBS) -pthread -fopenmp 

