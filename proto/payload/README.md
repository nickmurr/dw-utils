```makefile
.PHONY: protoc-gen
protoc-gen:
	GOBIN=$(CURDIR)/bin go install \
		github.com/golang/protobuf/protoc-gen-go \
		github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2 \
		github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-grpc-gateway \
		github.com/rakyll/statik \
		github.com/gogo/protobuf/protoc-gen-gofast \
		github.com/gogo/protobuf/proto \
        github.com/gogo/protobuf/jsonpb \
        github.com/gogo/protobuf/protoc-gen-gogo \
        github.com/gogo/protobuf/gogoproto \


PROTOM := Mgoogle/protobuf/any.proto=github.com/gogo/protobuf/types,Mgoogle/protobuf/duration.proto=github.com/gogo/protobuf/types,Mgoogle/protobuf/struct.proto=github.com/gogo/protobuf/types,Mgoogle/protobuf/timestamp.proto=github.com/gogo/protobuf/types,Mgoogle/protobuf/wrappers.proto=github.com/gogo/protobuf/types,


.PHONY: generate-payload
generate-payload:
	mkdir -p $(CURDIR)/pkg/pb/ && \
	protoc \
		--plugin=protoc-gen-gofast=$(CURDIR)/bin/protoc-gen-gofast \
		-I$(CURDIR)/dw-utils/proto \
		--gofast_out=$(PROTOM),plugins=grpc:. \
		$(CURDIR)/dw-utils/proto/payload/payload.proto
		-dest=$(CURDIR)/pkg/pb/payload/ \
		-src=$(CURDIR)/pkg/pb/payload/
		
.PHONY: generate-schedule
generate-schedule:
	mkdir -p $(CURDIR)/pkg/pb/ && \
	protoc \
		--plugin=protoc-gen-gofast=$(CURDIR)/bin/protoc-gen-gofast \
		-I$(CURDIR)/dw-utils/proto \
		--gofast_out=$(PROTOM),plugins=grpc:. \
		$(CURDIR)/dw-utils/proto/payload/schedule.proto
		-dest=$(CURDIR)/pkg/pb/schedule/ \
		-src=$(CURDIR)/pkg/pb/schedule/
```
