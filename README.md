/*
* Copyright (c) 2023 Guangzhou University.
*
* Licensed under the Apache License, Version 2.0 (the "License");
* you may not use this file except in compliance with the License.
* You may obtain a copy of the License at:
*
*     http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
* See the License for the specific language governing permissions and
* limitations under the License.
*/

/*
* Name: Evaluation of Partitions in Packet Classification
* Version: 1.0
* Author: Xinyao
* Email: xinyao@gzhu.edu.cn
* Date: 11.16, 2023
* This code refers to the literature [1].
* [1] wenjun Li, Tong Yang, Ori Rottenstreich, Xianfeng Li, Gaogang Xie, Hui Li, Balajee Vamanan, Dagang Li and Huiping Lin, “Tuple Space Assisted Packet Classification with High Performance on Both Search and Update,” In Special Issue on Network Softwarization & Enablers，IEEE Journal on Selected Areas in Communications (JSAC), 2020.
*/

Tested on Ubuntu 22.04.1 LTS 

Requirement:
g++ at least version 4.9.


Before using, please place the dataset (for example, the entire "rules" folder) into each algorithm folder separately.

**1. CutSplit:**
Modify the partition step based on the original algorithm. Change the threshold setting based on the prefix threshold method from (t, t) to (t_1, t_2). The resulting throughput is presented in column vector form (specifically, by first fixing t_1, traversing t_2, then letting t_1 traverse and repeating the above process). The results are stored in the result.csv file.
Usage Example:
./run.sh ./rules/acl1_1k ./rules/acl1_1k_trace

**2. PHyperSplit:**
On the basis of the CutSplit algorithm, eliminate the FiCuts step, retaining only the partition + split steps. The threshold setting and result format are the same as above. The results are saved in the corresponding result.csv file.
Usage Example:
./run.sh  ./rules/acl1_1k  ./rules/acl1_1k_trace

**3. Modularity:**
Perform the same partition steps as described above, then establish a graph-theoretic model of rule overlap. Evaluate the partition results using the Disassortative Modularity metric. The results are saved in the QH.txt file.
Usage Example:
mkdir build
cd build
cmake .. && make && ../bin/Modularity GA -r ../rules/acl1_1k  -p ../rules/acl1_1k_trace



