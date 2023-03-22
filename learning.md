# What I learnt

## runtime package

runtime package "k8s.io/apimachinery/pkg/runtime" provides utitlies that can be used to manage runtime objects. Runtime objects are Go structs that represent kubernetes objects. But since Kubernetes itself prefers JSON or YAML, The package bridges the gap between Go code and YAML/JSON.

## Scheme package

As we know, objects are present in form of YAML/JSON in kubernetes and also has various fields like metadata, spec etc, but in form of Go structs in Go code. Managing the connectivety can be tedious, therefore scheme package provides a mapping between them to make things easier.

## Why adding core types into the scheme ?

When we create a Custom Resrouce, we have to register it with the kuberntes API server, which is "Adding the new schmea to the existing schema", the resource itself might referece/use core types like deployments, pods etc. So we package them together with the custom type.

## Groups, Versions, Kinds and Resources (Oh my!)

Group is just grouping up of functionality, and versions help to understand how they evolved over time.

Kind is an object type, it is used to categorize objects. A resource on the other hand is a concrete instance of a kind. Example, A deployment is a type in kubernetes, but when we create a deployement (let's say myapp), it a resource which itself is a instance of that object.

here is the entire flow, you create a group, that is going to contain Kinds, that are nothing but definitions of what a specific "Kind" is supposed to do. There can be different versions of same group, that may have different functionalities. Then come resources, they are created when we use one of the kinds to create something more specific.

A pod is a kind present in the core group (v1.Pod), but a pod running an application (let's say myapp) is a resource of Pod kind.

Next, we create Custom Resource Definitions as Go structs, that define how the custom resource looks like. Controllers are there to manage the instances of these CRDs.

Scheme is a way to keep track of which Go type corresponds to a given GroupVersionKind(GVK): A kind in a particular group-version.

## GroupVersionKind

It is made of three words, group, version and kind. It is a system that helps you to find what you need, in kubernetes, you need something to uniquely identify a resource. It can be done using GroupVersionKind. Group tells the API group to which the instance belongs. Since there can be many versions of the same API group name, you can specify the version as well. finally comes the Kind of the instance.

So if you create a new Custom Resource, you would have to give it a API group, an API version and a kind to uniquely identify it in the cluster.
