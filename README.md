# QuantumBusiness
from pyqpanda import *

# 1. THE "ENVELOPE": Your Digital Passport
# You get these from your dashboard at qcloud.originqc.com.cn
api_key = "YOUR_SECRET_API_KEY_HERE"

# 2. THE "MAILBOX": Connecting to the Cloud machine
# We use 'QMachineType.CLOUD' instead of 'CPU'
qvm = CloudQVM()
qvm.init_qvm(api_key)

# 3. THE "LETTER": (Your exact same logic from before)
qubits = qvm.qAlloc_many(2)
cbits = qvm.cAlloc_many(2)
prog = QProg()
prog << H(qubits[0]) << CNOT(qubits[0], qubits[1])
prog << measure_all(qubits, cbits)

# 4. THE "DELIVERY": Sending it to the Wukong Chip
# 'RealChip_Wukong' is the name of the 72-qubit destination
result = qvm.full_amplitude_measure(prog, 1000) 
# Note: For real hardware, you specify the chip name in the cloud settings
print(result)

qvm.finalize() 
