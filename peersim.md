# PeerSim

## Steps (Build Artifact)

  1. `curl -L -o jep-djep-2.3.1.zip https://sourceforge.net/projects/jep/files/jep-djep-2.3.1.zip/download`

  2. `unzip jep-djep-2.3.1.zip`

  3. ``export jep_dir=`pwd```

  3. `svn checkout https://svn.code.sf.net/p/peersim/code/trunk peersim-code` 

  4. `cd peersim-code/peersim`

  5. ``export peersim_dir=`pwd```

  6. `cp $jep_dir/djep-1.0.0.jar $peersim_dir/`

  7. `cp $jep_dir/jep-2.3.1.jar $peersim_dir/`

  8. `ln -s $peersim_dir/jep-2.3.1.jar $peersim_dir/jep-2.3.0.jar` 

      * This is because Makefile refers to jep-2.3.0.jar, but only 2.3.1 is available for download

  9. `make release`

## Tutorial

### Cycle Based

  1. Read Config

  2. Simulator

      2.1 setups the network

      2.2 initializes the nodes in the network

          * An instance per node

          * The instances of nodes and the protocols are created by cloning


  3. *Control* setup the initial states of *Protocol*

# Dependencies 

  * JEP 2.3.0[4] (this is the version used by PeerSim source code in trunk)

# References

  [1]. [A Java library for parsing, evaluating mathematical equations.](https://www.singsurf.org/)

  [2]. https://sourceforge.net/projects/jep/

  [3]. http://www.singularsys.com/jep/

  [4]. [JEP and DJEP binary](https://sourceforge.net/projects/jep/files/jep-djep-2.3.1.zip/download)

  [5]. [PeerSim HOWTO: Build a new protocol for the PeerSim 1.0 simulator](http://peersim.sourceforge.net/tutorial1/tutorial1.html)
