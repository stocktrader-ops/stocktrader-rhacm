# Issues

## Import cluster issues

### x509: certificate signed by unknown authority in registration pod on managed cluster




IBM ROKS cluster uses a signed custom CA certificate however due to the unique nature of the master nodes (that it is running as pod in another cluster)
the kubeapiserver controller is disabled and the resource was not configured to contain the CA cert information 

from managed cluster import controller's perspective it seems as if the hub does not have an custom CA cert 
(which is incorrect in this case but given then information that it have access to it have no way of knowing that) and uses the self sign CA for the agent to communicate with the hub

the current proposed solution to IBM is that ROKS should configure `kubeapiserver` resource with the proper
information (even tho the resource itself is not being acted upon by the kube apiserver controller) and 
thus give managed cluster import controller a way to determine the correct CA

G2Bsync 729717693 comment 
 juliana-hsu Wed, 18 Nov 2020 14:32:15 UTC 
 G2Bsync   Hao Liu:  ROKS hub is not supported.  ROKS spoke is supported
