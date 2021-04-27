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
        github.com/mwitkow/go-proto-validators \


PROTOM := Mgoogle/protobuf/any.proto=github.com/gogo/protobuf/types,Mgoogle/protobuf/duration.proto=github.com/gogo/protobuf/types,Mgoogle/protobuf/struct.proto=github.com/gogo/protobuf/types,Mgoogle/protobuf/timestamp.proto=github.com/gogo/protobuf/types,Mgoogle/protobuf/wrappers.proto=github.com/gogo/protobuf/types,
PROTOPATH := dw-utils
GOGOPROTO = -I=${GOPATH}/src -I=${GOPATH}/src/github.com/gogo/protobuf/protobuf



.PHONY: generate-slack-integration
generate-slack-integration:
	mkdir -p $(CURDIR)/pkg/pb/ && \
	protoc \
		-I=. $(GOGOPROTO) \
		--plugin=protoc-gen-gofast=$(CURDIR)/bin/protoc-gen-gofast \
		-I$(CURDIR)/$(PROTOPATH)/proto \
		--gofast_out=$(PROTOM),plugins=grpc:. \
		$(CURDIR)/$(PROTOPATH)/proto/slack_integration/slack_integration.proto
		-dest=$(CURDIR)/pkg/pb/slack_integration/ \
		-src=$(CURDIR)/pkg/pb/slack_integration/
```
