```makefile
proto_indexing:
	mkdir -p $(CURDIR)/pkg/pb/indexing
	protoc \
	-I=dw-utils/proto/indexing indexing.proto \
	--go_out=$(PROTOM),plugins=grpc:. \
```
