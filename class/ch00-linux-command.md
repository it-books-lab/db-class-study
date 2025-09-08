# Linux command 자주 쓰는 명령어

```
pwd
ls [-l]
cd <dir>
cd ..
cd ~
mkdir <dir>
cp <filename> <dir>: 복사 | cp <origin_file_name> <new_file_name>: 이름 바꾸기
mv <oldname> <newname>: 이름 바꾸기 | move <filename> <dir>: 이동
rm <filename>
rmdir <directory>
rm -r <directory>: 해당 디렉토리를 포함한 안에 있는 모든 파일 삭제
cat <filename> [<filename>, <filename>, ...]
chmod +x <filename>
less/more <filename>: cat이랑 비슷한 기능.
man <keyword>
which <keyword>
grep <String> <filename>
find <dir> -n '*.txt'
clear
finger <username>
groups
who
whoami
```

## rm

- rm 파일만 삭제: rm dir4/dir5/dir6/combined.txt combined_backup.txt
- rmdir 빈 폴더만 삭제
- rmdir -p f1/f2/f3: 상위에 있는 빈 폴더들 삭제
- rm -r folder(folder에 있는 폴더와 파일 삭제): rm -r folder_6
- 한 번 삭제하면 복구 불가 → 안전 삭제 방법: rm -i filename

## cp, mv

- cp [file] [where] or cp [origin_file] [copy_file]같은 디렉토리에 다른 이름으로 복사
- mv [oldname] [newname]: 같은 디렉토리에 있을 때 이름 바꾸기
- mv [file] [where]: file을 dir(where)로 옮기기

## which

```
which python
```

- `python` 실행 파일의 경로(`/usr/bin/python` 등)를 출력
- 실행 가능한 명령어(프로그램)가 **어느 경로에 있는지** 확인

## grep

```
grep "error" logfile.txt

→ logfile.txt 안에서 "error"라는 단어가 포함된 줄만 출력
```

- 파일이나 출력 내용에서 **특정 문자열(패턴)** 검색

## find

```
find /home -name "*.txt"

→ /home 디렉토리 아래에서 확장자가 .txt인 파일을 모두 찾음
```

- 디렉토리 안에서 **조건에 맞는 파일/디렉토리 검색**

## clear

- 터미널 화면을 깨끗하게 지움

## finger

```
finger <username>

→ username 사용자의 정보 표시
  (일부 시스템에는 기본 설치 안 되어 있음! sudo apt install finger로 설치해야 함)
```

- 사용자의 로그인 정보, 홈 디렉토리, 쉘, 접속 상태 등을 확인

## groups, who, whoami

- groups: 현재 사용자가 속한 **그룹 정보** 확인
- who: 현재 시스템에 로그인한 사용자 확인
- whoami: 현재 로그인한 **사용자의 계정 이름** 출력

# Linux command 권한 설정

리눅스 파일 권한은 **특수비트 3개 + 소유자(owner), 그룹(group), 기타(others)** 각각의 **r/w/x** 3개씩 — 총 12비트(실제로는 파일 타입 필드까지 포함하면 더 많음)로 관리.

- 특수비트: `setuid`, `setgid`, `sticky`
- 권한비트(각 3비트): `r`(읽기)=4, `w`(쓰기)=2, `x`(실행)=1

---

# 2) 절대(숫자) 모드

숫자 3자리(또는 특수비트를 포함하면 4자리)로 권한을 표현.

- 각 자리(오른쪽부터): **others**, **group**, **owner** (각 자리: 0~7)
- 각 자리는 r=4, w=2, x=1 을 더한 값
- 특수비트(선행 자리, optional): setuid=4, setgid=2, sticky=1 (따라서 4자리 예: `4xxx`, `2xxx`, `1xxx`)

예: `chmod 754 file`

- owner: `7 = 4 + 2 + 1` → `rwx`
- group: `5 = 4 + 0 + 1` → `r-x`
- others: `4 = 4 + 0 + 0` → `r--`
    
    따라서 `754` → `rwx r-x r--`
    

다음은 자주 쓰이는 숫자들 (읽기 쉬운 표):

```
7 -> rwx
6 -> rw-
5 -> r-x
4 -> r--
3 -> -wx
2 -> -w-
1 -> --x
0 -> ---

```

### 실제 명령

```bash
chmod 755 script.sh     # owner rwx, group r-x, others r-x
chmod 4755 /usr/bin/someprog  # setuid + 755

```

---

# 2) 심볼릭(Symbolic) 모드

### 기호(symbolic) 방식

- `u` = owner(user), `g` = group, `o` = others, `a` = all
- `+`, , `=` 연산자 사용

```bash
chmod u+x script.sh      # owner에 실행권 추가
chmod g-w file.txt       # group의 쓰기권 제거
chmod o=r file.txt       # others를 읽기만으로 설정
chmod a=rw file.txt      # 모든 사용자에게 rw로 설정

```

---

```
chmod -R 755 mydir
-R: 디렉토리 mydir과 그 안의 모든 하위 파일·디렉토리까지
```
