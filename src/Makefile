CC		= g++
CC_FLAGS	= -Wall -O3 -static-libgcc -static-libstdc++ -fopenmp -DHAVE_INLINE
LD_FLAGS	= -lgsl -lgslcblas
prefobj		= emission.o common-functions.o
filterHDobj	= emission.o common-functions.o jump-diffusion.o minimization.o
cloneobj	= clone.o clone-bulk.o clone-prior.o clone-llh.o clone-predict.o clone-update.o clone-fwd-bwd.o
cloneHDobj	= $(cloneobj) emission.o common-functions.o minimization.o log-space.o cloneHD-functions.o cloneHD-inference.o
.PHONY: clean all
all: preFilter filterHD cloneHD
	rm -rf ./*.o
preFilter: $(prefobj) pre-filter.o
	$(CC) $(CC_FLAGS) $^ -o pre-filter $(LD_FLAGS)
filterHD: $(filterHDobj) filterHD.o
	$(CC) $(CC_FLAGS) $^ -o filterHD $(LD_FLAGS)
cloneHD: $(cloneHDobj) cloneHD.o
	$(CC) $(CC_FLAGS) $^ -o cloneHD $(LD_FLAGS)	
%.o: %.cpp
	$(CC) $(CC_FLAGS) -c $< -o $@
$(cloneobj): clone.h# $(cloneobj:.o=.cpp)
$(filterHDobj) $(cloneHDobj) $(prefobj): $(.TARGET:.o=.h)
clean:
	rm -rf ./*.o
