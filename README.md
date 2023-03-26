# 최신 ARM64 리눅스 커널 5.19 분석

## 커뮤니티: IAMROOT 19차
- [www.iamroot.org][#iamroot] | IAMROOT 홈페이지
- [jake.dothome.co.kr][#moonc] | 문c 블로그

[#iamroot]: http://www.iamroot.org
[#moonc]: http://jake.dothome.co.kr

## \# How to build and run
```
$ sudo apt install -y build-essential gcc-aarch64-linux-gnu g++-aarch64-linux-gnu git bison flex libssl-dev libncurses-dev  
$ make CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm64 arm64_qemu_defconfig
$ make CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm64
$ sudo apt install -y qemu-system-arm
```
-> [rootfs download](http://downloads.yoctoproject.org/releases/yocto/yocto-4.0/machines/qemu/qemuarm64/core-image-minimal-qemuarm64-20220416133845.rootfs.ext4)
```
sudo qemu-system-aarch64 -M virt -smp 4 -m 1024 -cpu cortex-a57 -nographic \
  -kernel linux/arch/arm64/boot/Image \
  -append 'root=/dev/vda rw rootwait mem=1024M loglevel=8 console=ttyAMA0' \
  -netdev user,id=net0 \
  -device virtio-net-device,netdev=net0 \
  -drive if=none,id=disk,file=core-image-minimal-qemuarm64-20220416133845.rootfs.ext4,format=raw \
  -device virtio-blk-device,drive=disk
```
## \# History

- 첫 모임: 2022년 5월 7일 (zoom online)

### 44주차 
- 2023.03.25 Zoom 온라인
- ARM 리눅스 커널 4.2 memblock_double_array() ~ 4.3 전까지 코드분석, 3.1 ~ 3.1.3 map_kernel() 책 읽기 (~137쪽)

### 43주차 
- 2023.03.18 Zoom 온라인
- ARM 리눅스 커널 4.1.4 ~ 4.2 memblock_double_array() 코드분석 (~237쪽)

### 42주차 
- 2023.03.12 Zoom 온라인
- ARM 리눅스 커널 4.3.3 vmemmap을 사용하는 sparse 메모리모델 (~304쪽)

### 40주차, 41주차
- 2023.02.24, 2023.03.04. Zoom 온라인
- ARM 리눅스 커널 4.3.2 부트 메모리 초기화
- 41주차에는 40주차에 스터디한 내용을 복습했습니다.

### 39주차
- 2023.02.18, Zoom 온라인 (10명 참석)
- ARM 리눅스 커널 4.1.4 memblock 추가 ~ 4.3.1 존 타입

### 38주차
- 2023.02.11, Zoom 온라인 (9명 참석)
- ARM 리눅스 커널 3.5 vmemmap ~ 4.1.3 memblock 할당과 해제
- vmemmap_populate() 분석 완료

### 37주차
- 2023.02.04, Zoom 온라인 (10명 참석)
- ARM 리눅스 커널 3.4 I/O 메모리 매핑(ioremap) 읽음
- ioremap 관련 함수 분석 완료

### 36주차
- 2023.01.28, Zoom 온라인 (8명 참석)
- vunmap() 분석 완료
- ARM 리눅스 커널 3.4 ~ 3.4.1 ioremap

### 36주차
- 2023.01.21
- 명절 휴식

### 35주차
- 2023.01.14, Zoom 온라인 (8명 참석)
- vmap() 분석 완료
- vunmap() 분석 예정

### 34주차
- 2023.01.07, Zoom 온라인 (9명 참석)
- vmap() 분석 중
- vmap()->get_vm_area_caller()->alloc_vmap_area()->insert_vmap_area() 분석 완료
- vmap()->get_vm_area_caller()->alloc_vmap_area()->purge_vmap_area_lazy() 분석 예정

### 33주차
- 2022.12.31, Zoom 온라인 (7명 참석)
- ARM 리눅스 커널 3.3.3 vmap_area 할당 ~ 3.3 끝
- vmap() 분석 중
- vmap()->get_vm_area_caller()->alloc_vmap_area() 분석 완료
- vmap()->get_vm_area_caller()->alloc_vmap_area()->__alloc_vmap_area 분석 예정

### 32주차
- 2022.12.24
- 크리스마스 휴식

### 31주차
- 2022.12.17, Zoom 온라인 (11명 참석)
- ARM 리눅스 커널 3.3.3 vmap_area 할당 ~ 3.3.4 vunmap

### 30주차
- 2022.12.10, Zoom 온라인 (11명 참석)
- MM Overview Seminar (유형곤)
- ARM 리눅스 커널 3.3.1 ~ 3.32 vmap

### 29주차
- 2022.12.03, Zoom 온라인 (7명 참석)
- MM Overview Seminar (유형곤)

### 28주차
- 2022.11.26, Zoom 온라인 (9명 참석)
- MM Overview Seminar (유형곤)

### 27주차
- 2022.11.19, 오프라인 (3명 참석), Zoom 온라인 (5명 참석)
- IARMROOT 16기 Seminar 참석
- start_kernel 이후 스터디 방법 재논의
- struct thread_info 분석

### 26주차
- 2022.11.12, Zoom 온라인 (9명 참석)
- start_kernel 시작
- local_irq_disable까지 분석 완료
- start_kernel 이후 스터디 방법 논의

### 25주차
- 2022.11.05, Zoom 온라인 (7명 참석)
- init_feature_override, kaslr_early_init, switch_to_vhe 분석 완료

### 24주차
- 2022.10.29, Zoom 온라인 (8명 참석)
- early_fixmap_init@arch/arm64/mm/mmu.c 분석 완료
- fixmap_remap_fdt@arch/arm64/mm/mmu.c 분석 완료
- early_fdt_map@arch/arm64/kernel/setup.c 분석 완료

### 23주차
- 2022.10.22, Zoom 온라인 (6명 참석)
- ARM리눅스커널 3.1.2, 3.2.1
- __primary_switched - early_fdt_map 분석 중

### 22주차
- 2022.10.15, Zoom 온라인 (8명 참석)
- __primary_switched 분석 중
- arch/arm64/kernel/entry.S Exception 관련 내용 분석 중 (kernel_ventry)

### 21주차
- 2022.10.08, Zoom 온라인 (8명 참석)
- __primary_switch 분석 완료
- __primary_switched 분석 시작

### 20주차
- 2022.10.01, Zoom 온라인 (6명 참석)
- __cpu_setup@arch/arm64/mm/proc.S 완료
- __primary_switch 분석 시작

### 19주차
- 2022.09.24, Zoom 온라인 (13명 참석)
- __cpu_setup@arch/arm64/mm/proc.S 진행 중

### 18주차
- 2022.09.17, Zoom 온라인 (7명 참석)
- .macro map_memory, .macro compute_indices, .macro populate_entries 완료
- ARM리눅스커널 2.1.5 CPU 초기화
- __cpu_setup@arch/arm64/mm/proc.S 분석 시작

### 17주차
- 2022.09.03, Zoom 온라인 (14명 참석)
- __create_page_tables 완료

### 16주차
- 2022.08.27, Zoom 온라인 (11명 참석)
- 코드로 알아보는 ARM 리눅스 커널 : 2.1.3 ~ 2.1.4
- set_cpu_boot_mode_flag 완료
- __create_page_tables 분석 시작
- **Discord 새로 시작**

### 15주차
- 2022.08.20, Zoom 온라인
- 코드로 알아보는 ARM 리눅스 커널 : 2.1 ~ 2.1.2
- dcache_inval_poc, init_kernel_el 완료

### 14주차
- 2022.08.13, Zoom 온라인
- 첫 Linux kernel v5.19 source code 분석 시작
- preserve_boot_args 완료
