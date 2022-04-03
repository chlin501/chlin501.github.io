# Rights Amplification  

Rights Amplification takes both the sealed message and the unsealer to have the authority to read the message (which may, of course, contain more capabilities). 

## Sealer/ Unsealer pattern 

### Sample

    ```
    // See [2][3]
    final case class Brand private(...) {
        trait Sealer
        trait Unsealer
    }
    ```

### Applications

* Secure a dataflow

* Track 'responsibility' 

* ACLs

# References

[1]. https://wiki.c2.com/?RightsAmplification= 

[2]. https://gitorious.org/repo-roscidus/e-core/blobs/fdf9643e419eea182b4d8d983f5b9955c7b73967/src/jsrc/org/erights/e/elib/sealing/SealedBox.java?p=repo-roscidus:e-core.git;a=blob;f=src/jsrc/org/erights/e/elib/sealing/SealedBox.java;h=7ece34b9137e305a529bf9a5a0b6aa1246f3886e;hb=HEAD

[3]. https://gitorious.org/repo-roscidus/e-core/blobs/fdf9643e419eea182b4d8d983f5b9955c7b73967/src/jsrc/org/erights/e/elib/sealing/SealedBox.java?p=repo-roscidus:e-core.git;a=blob;f=src/jsrc/org/erights/e/elib/sealing/Brand.java;h=ce399b4b45c5d7b7730ea84799fba1eef691e010;hb=HEAD
