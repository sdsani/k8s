## Referances
| Link                                         | Description |
| -------------------------------------------- |:----------------------------------------:|
| https://github.com/bmuschko/cks-crash-course | CKS Crash Cource material                | 
| https://www.youtube.com/watch?v=gcz5VsvOYmI  | The Hitchhiker's Guide to Pod Security - Lachlan Evenson, Microsoft|
| https://www.youtube.com/watch?v=v6a37uzFrCw  | Kubernetes security best practice by Ian Lewis|
| https://kubernetes.io/docs/tutorials/security/ns-level-pss/| Example |
| https://www.appvia.io/blog/podsecuritypolicy-is-dead-long-live| Another good article on PSS |

## Keep in mind
1. Applied at name space level 
1. No direct parity with Pod security policy  
1. No mutation  
1. Pod security policy will be removed in K8S 1.25  
1. Pod admission is the way to go now  
1. Other options gatekeeper, Kyverno    
1. Built in admission controller  
1. Levels available are privileged, baseline, restricted. More details; https://kubernetes.io/docs/concepts/security/pod-security-standards/
1. Modes available are enforce, audit, warn. https://kubernetes.io/docs/concepts/security/pod-security-admission/  
1. Feature is turned on starting 1.23  

## Sample labels to apply to a namespace
pod-security.kubernetes.io/<MODE>-version:<level>   (k8s version is optional and default value is latest)

## Commands used  
| Command                                              | Description |
| ---------------------------------------------------- | ---------------------------------------- |
| kubectl version                                      | Current version                          |
| kubectl get nodes                                    | Get nodes in cluster                     |
| kubectl get namespaces                               | List of all name spaces                  |
| kubectl -n kubect-system exec \ <br>kube-apiserver-control-plane -it \ <br> -- kube-apiserver -h \| grep \ <br> "default enabled ones"| Check status of the Pod security feature|
| kubectl apply -f playgroundns-warn-basel.yaml        ||
| kubectl apply -f priviliged-pod.yaml -n playground   ||
| kubectl apply -f priviliged-pod.yaml --dry-run=server||
| kubectl get --raw /metrics | grep pod_security_evaluations_total|What voilations we are hitting and how many times|

