## ICC2 ( IC Compiler II)

* IC Compiler II is specifically architected to address aggressive performance, power, area (PPA), and time-to-market pressures of leading edge designs.
  
* Key technologies include a pervasively parallel optimization framework, multi-objective global placement, routing driven placement optimization, full flow Arc based concurrent clock and data optimization, total power optimization, multi-pattern and FinFET aware flow and machine learning (ML) driven optimization for fast and predictive design closure.
  
* Advanced Fusion technologies offer signoff IR drop driven optimization, PrimeTime® delay calculation within IC Compiler II, exhaustive path based analysis (PBA) and signoff ECO within place and route for unmatched QoR and design convergence. 

![image](https://github.com/user-attachments/assets/bf363650-49b3-48b4-b64a-5d7bcebbab02)

* The `IC Compiler II` tool is designed for efficient design planning, placement, routing, and analysis of very large designs.
  
* IC Compiler II is a complete netlist-to-GDSII implementation system that includes early design exploration and prototyping, detailed design planning, block implementation, chip assembly and sign-off driven design closure.
  
* The foundation, architecture and implementation is based on novel, patented technologies and the software has been written using modern object-oriented languages and tools.
  
* IC Compiler II benefits from the combination of a new hierarchical infrastructure enabling massive parallelism; a highly compact multi-corner and multi-mode (MCMM) architecture; next-generation design-planning; new global, analytical, and scalable optimization techniques; and global optimization approaches to clock synthesis.
  
* `Design planning` is an integral part of the `RTL to GDSII design process`. During design planning, you assess the feasibility of different implementation strategies early in the design flow.
  For large designs, `design planning` helps you to “divide and conquer” the implementation process by partitioning the design into smaller, more manageable pieces for more efficient processing.
  
* IC Compiler is for place and route and it is used after synthesis which can be done with Synopsys DC compiler or Power compiler. IC Compiler goes through the following steps and its outputs go to tapeout.

![image](https://github.com/user-attachments/assets/b19633b4-bae0-4c58-8d8d-339916a8168f)

* IC Compiler three initialization Files

![image](https://github.com/user-attachments/assets/4404c6c2-cc11-45e2-a237-a3829ebeb2c3)

* Summary

![image](https://github.com/user-attachments/assets/9645bc4f-9273-4a1c-a45d-6f29d5ade61f)


* The `target_library` is the library that IC Compiler uses to pick cells for optimization and re-mapping. It is typically set to only the standard cells library.
  
* The `link_library` contains every library that contains cells that are referenced by the netlist.

1. Milkyway Reference Libraries 
Information is stored in so-called “views”, for example: 
   * CEL: The full layout view 
   * FRAM: The abstract view used for P&R 
   * LM: Logic Model with Timing and Power info (optional*) 。(Optional) here means that the logical libraries do not have to be stored within the Milkyway library structure, but can be located 
     anywhere else. IC Compiler only reads logical libraries (.db) specified through the link_library variable. 
 
2. Technology File (.tf file) 
   * Tech File is unique to each technology
   * Contains metal layer technology parameters:
     *  Number and name designations for each layer/via
     *  Dielectric constant for technology
     *  Physical and electrical characteristics of each layer/via
     *  Design rules for each layer/Via (Minimum wire widths and wire-to-wire spacing, etc.)
     *  Units and precision for electrical units
     *  Colors and patterns of layers for display 

* Example of a Technology File: 

```
Technology  { 
  dielectric  = 3.7 
  unitTimeName  = "ns" 
  timePrecision  = 1000 
  unitLengthName  = "micron" 
  lengthPrecision  = 1000 
  gridResolution  = 5 
  unitVoltageName  = "v" 
  } 
... 
Layer  "m1" { 
  layerNumber  = 16 
  maskName   = "metal1" 
  pitch   = 0.56 
  defaultWidth  = 0.23 
  minWidth   = 0.23 
  minSpacing  = 0.23 

```

* ICC Design Planning Flow

![image](https://github.com/user-attachments/assets/d1d9948a-95cf-4571-b572-8eeb80d3d517)
