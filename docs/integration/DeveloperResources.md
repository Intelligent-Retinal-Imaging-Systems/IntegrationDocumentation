---
title: Developer Resources
nav_order: 5
---

# Developer Resources
IRIS Provides examples and libraries for cloud direct integrations.  

- Coding examples can be found on github
- Source code can be found on github
- Libraries are made accessible through online repositories relative to the development environment



# Microsoft DotNetCore / Visual Studio / C#
Integration in the Microsoft environment is made available from the NuGet public repository.

## Packages

| Name | Details
| -- | -- |
| Iris.Public.Types | Contains models for all transactions.  This can be used directly if you want to build your objects, serialize and perform cloud operations on your own.
| Iris.Public.Order | Encapsulates cloud operations related to submitting and monitoring order status
| Iris.Public.Result.Azure | If results are received on an IRIS Cloud resource, this library encapsulates cloud operations. Start a listener and wait for results to pop.
| Iris.Public.Image | Encapsulates process of pushing images to IRIS when using cameras that are not directly integrated to IRIS. 
| Iris.Public.Grading | Test environment only library for grading your own orders.  Allows you to do extensive debugging with your new code. 


# Typescript 
Typescript packages are available from NPM as well you can access the public github repo for the code directly. 

https://github.com/Intelligent-Retinal-Imaging-Systems/ts-service-bus

# Node / NPM
See typescript


# GOLANG
Code examples and source code can be found at https://github.com/Intelligent-Retinal-Imaging-Systems/iris-cloud-direct-go