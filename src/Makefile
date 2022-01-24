all:
	g++ -std=c++11 centralized_with_indexing.cpp -o cen_idx -lpthread
	g++ -std=c++11 centralized.cpp -o cen -lpthread
	g++ -std=c++11 decentralized.cpp -o decen -lpthread
clean:
	rm ./cen_idx ./cen ./decen
