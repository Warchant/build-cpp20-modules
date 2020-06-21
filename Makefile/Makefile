CXX=clang++
FLAGS=-std=c++2a -stdlib=libc++ -fmodules

SRCS=../src/main.cpp \
	../src/module1.cpp

PCM=../src/module1.pcm

%.pcm: %.cpp
	@echo Precompile module $<
	$(CXX) $(FLAGS) -c $< -Xclang -emit-module-interface -o $@

$(PCM): $(SRCS)

.PHONY: all
all: $(PCM)
	$(CXX) $(FLAGS) -fbuiltin-module-map -fimplicit-module-maps -fprebuilt-module-path=../src -o main $(SRCS)
	./main

.PHONY: clean
clean:
	@echo "Cleaning..."
	rm -rf $(PCM)
	rm -rf *.o
	rm -f main