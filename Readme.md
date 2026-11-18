MongoDB Replica Set — Automated Deployment & Rolling Upgrade with Ansible

Môi trường: 5 AWS EC2 (Ubuntu 22.04), MongoDB Replica Set rs0, quản lý bằng Ansible trên Ubuntu WSL.

Phần I. Chiến lược triển khai bằng Ansible

1. Initial Deployment — Cài đặt MongoDB

Playbook: install-mongodb.yml

Cài đặt MongoDB 6.0.30 trên cả 5 EC2, khởi động dịch vụ mongod và xác minh 5/5 node hoạt động thành công.

2. Replica Set Configuration — Thiết lập Replica Set

Playbook: configure-replicaset.yml

Cấu hình Replica Set rs0 với 1 PRIMARY (mongo1) và 4 SECONDARY, sử dụng Private IP để giao tiếp giữa các node.

3. Rolling Upgrade — Nâng cấp MongoDB

Playbook: upgrade-mongodb.yml

Nâng cấp lần lượt 4 SECONDARY trước, sau đó rs.stepDown() để chuyển PRIMARY và nâng cấp mongo1 cuối cùng. Kết quả: 5/5 node chạy MongoDB 7.0.48, failed=0.

