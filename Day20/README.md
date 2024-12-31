## ECO using Prime Time

<details>
  <summary>ECO in VLSI Design</summary>
  <br>
  
* ECO stands for `Engineering Change Order` in the context of VLSI (Very Large Scale Integration) design.
  
* It refers to a formalized process for implementing changes in a hardware design after the initial design has been completed.
  
* ECOs are often used to address issues such as bugs, performance improvements, or changes in specifications that occur after the design has been finalized but before or after fabrication.

## Purpose of ECO:

* To correct errors or defects in the original design.
  
* To implement functional changes or enhancements.
  
* To accommodate changes in specifications or requirements.

## ECO Process

* `Identification:` The need for an ECO is identified, often through testing, simulation, or customer feedback.
  
* `Assessment:` Engineers assess the impact of the proposed changes on the overall design, including compatibility, functionality, and timing.
  
* `Modification:` The design is modified according to the ECO, which may include changes in the schematics, layout, or HDL (Hardware Description Language) code.
  
* `Verification:` The modified design undergoes verification through simulations and checks to ensure that the changes achieved the desired effects without introducing new issues.
  
* `Documentation:` The ECO process is documented for future reference, including the rationale for changes, the details of the modifications, and testing results.

## Types of ECO

#### The engineering change orders can be classified into two categories:

* `All layers ECO:` In this, the design change is implemented using all layers. This kind of ECO provides advantage in terms of cycle time and engineering costs.
  It is implemented whenever the change is not possible to be carried out without all layer change e.g. there is an updation in a hard macro cell or the change may require updation of 100’s of cells. It is almost impossible to contain such a large change to a few layers only.
  
* `Metal-only ECO:` Sometimes, it may not be practical to use all the layers (base + metal) to do the ECO. In that case, to minimize the cost, it is required to be completed with changes only in minimal number of metal layers. These days, it is expected that every design will be re-opened for the ECOs. So, an adequate number of spare cells are sprinkled during the implementation all over the design to be used later on. These cells are spread uniformly over the design. The inputs of these cells are tied. Whenever the need for an ECO arises, the cells to be implemented can be mapped into the existing spare cells. Hence, there is no need to change the base layers in such a case. Only the connections need to be updated which can be done by changing the metal layers only. Hence, the base layer cost is saved.


## Challenges in ECO:

* `Version Control:` Managing changes and keeping track of different design versions can be complex.
  
* `Integration:` Ensuring that the ECO does not negatively affect other parts of the design or the overall system.
  
* `Timing Analysis:` Changes might affect timing, requiring thorough timing analysis after modifications.

## Conclusion

ECO plays a significant role in adapting and refining hardware designs to keep up with evolving requirements and to resolve issues identified post-design.

</details>
