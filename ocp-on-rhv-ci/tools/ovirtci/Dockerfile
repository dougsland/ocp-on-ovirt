# This Dockerfile is used by ocp-on-rhv CI to publish the prFinder image
FROM registry.svc.ci.openshift.org/openshift/release:golang-1.14 AS builder
WORKDIR /go/src/github.com/oVirt/ocp-on-ovirt/ocp-on-rhv-ci/tools/ovirtci
COPY . .
RUN hack/build.sh


FROM registry.svc.ci.openshift.org/origin/4.1:base
COPY --from=builder /go/src/github.com/oVirt/ocp-on-ovirt/ocp-on-rhv-ci/tools/ovirtci/prFinder /bin/prFinder
RUN mkdir /output && chown 1000:1000 /output
USER 1000:1000
ENV PATH /bin
ENV HOME /output
WORKDIR /output
ENTRYPOINT ["/bin/prFinder"]
