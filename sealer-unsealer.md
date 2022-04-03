# Rights Amplification  

Rights Amplification takes both the sealed message and the unsealer to have the authority to read the message (which may, of course, contain more capabilities). 

## Sealer/ Unsealer pattern 

### Sample

    ```
    final case class Brand ... {
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
