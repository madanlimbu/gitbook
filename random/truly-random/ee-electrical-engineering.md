---
description: Basic reference to topics related to EE
---

# EE (Electrical Engineering)

## Topics

### **Basic**

Circuits, Ohm's Law, Kirchhoff's Laws (KVL, KCL), Nodal analysis (Node voltage method), Mesh current circuit analysis

**Current** - Flow of electron (_Amp_). The Current move from negatively charged to positive but as a convention for calculation, we assume it flows from positive to negative (Hole current).\
**Voltage** - Push that causes current to flow (_Volt_)\
**Resistance** - Opposes current flow (_Ohm_)\
**Ohm's law** - _V=IR_\
**KVL** - Sum of voltage in the loop is equal to zero\
**KCL** - Sum of current coming in and out on a node is equal to zero

#### Nodal analysis (Node voltage method)

1. Identify (Label) Essential node (more than 2 component connections)
2. Pick one of the Essential nodes as reference (Ground) from which voltages are measured
3. Node Voltage equation in reference to reference node we picked\
   \- KCL for all but the ground node\
   \- Note we assume current is always flowing out of the node (has higher voltage)
4. _(N - 1)_ numbers of node voltage equations required to describe the whole circuit

**Mesh current circuit analysis**

1. Create a mesh for each loop in a circuit
2. Use KVL for each mesh
3. Request N number of the equation where N = number of mesh/loop

_References_:\
[Kirchhoff's Laws\
](https://www.youtube.com/watch?v=2Zu3ppq3n8I)[Node voltage method](https://www.youtube.com/watch?v=-wCGiSNk5tw)\
[Mesh current analysis](https://www.youtube.com/watch?v=nC0PJqOJJ28)

### **Superposition, Thévenin and Norton**

_References:_\
__[https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-002-circuits-and-electronics-spring-2007/video-lectures/lecture-3/](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-002-circuits-and-electronics-spring-2007/video-lectures/lecture-3/)\
[https://www.youtube.com/watch?v=4qEaI4FpYpw](https://www.youtube.com/watch?v=4qEaI4FpYpw)

