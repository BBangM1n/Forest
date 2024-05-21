# Forest
## 게임 장르 : 3D 턴제 수집형 RPG
## 게임 소개 : 여러유형의 몬스터와 룬을 파밍하여 월드를 클리어하는 턴제 방식의 게임입니다.
## 개발 목적 : 평소에 좋아하던 턴제 게임 기능들을 직접 구현 했습니다.
## 사용 엔진 : UNITY 2022.3.15f1
## 개발 기간 : 2023.10.31 ~ 2024.03.10
## 사용 서드파티
- NewtonJSOn
- FireBase (Auth, DataBase)
## 포트폴리오 빌드 파일 
- [구글 드라이브 링크 (폰빌드)](https://drive.google.com/file/d/1Vlu0-TCDOu_4R6dct8ti3Sbd1dxhQFvo/view?usp=drive_link)
- [구글 드라이브 링크 (컴퓨터빌드)](https://drive.google.com/file/d/1Vlu0-TCDOu_4R6dct8ti3Sbd1dxhQFvo/view?usp=drive_link)
- 테스트용 계정 : 1234@1234.1 / 123412
- 빌드파일 실행 시 한글 경로가 있다면 접속이 안될수도 있으므로 주의 부탁드립니다.
## 포트폴리오 에셋 파일 
- [구글 드라이브 링크 (에셋파일)](https://drive.google.com/file/d/1Vlu0-TCDOu_4R6dct8ti3Sbd1dxhQFvo/view?usp=drive_link)
## 유튜브 영상 링크
- [유튜브 영상 링크](https://www.youtube.com/watch?v=v50233gSmvE)
## 주요 활용 기술
- #01)(스크립트) [Firebase이용한 로그인](https://cafe.naver.com/bbangnity/71)
<details>
<summary>적용 이미지</summary>
![로그인](./GitImage/로그인.gif)
</details>

***

- #02)(스크립트) [Firebase이용한 데이터베이스 관리](https://cafe.naver.com/bbangnity/86)
<details>
<summary>적용 코드</summary>
  
```
    public void LoadDB()  // 플레이어 데이터를 데이터베이스에서 불러오는 함수
    {
        // UserId에 있는 MonsterInventory 데이터를 데이터베이스에서 불러오기
        reference.Child(FireBaseAuthManager.Instance.UserId).Child("MonsterInven").GetValueAsync().ContinueWith(task =>
        {
            if (task.IsFaulted)
            {
                // 예외 처리
                Debug.LogError("Error getting data: " + task.Exception);
                return;
            }
            if (task.IsCompleted)
            {
                // 데이터를 JSON 형식으로 변환
                DataSnapshot snapshot = task.Result;
                string jsonData = snapshot.GetRawJsonValue();
                // JSON 데이터를 파일에 저장
                string filePath = MonsterDataManager.instance.playermonsterDataPath;
                File.WriteAllText(filePath, jsonData);
                // 파일에서 JSON 데이터 읽기
                string savedJsonData = File.ReadAllText(filePath);

                // JSON 데이터를 몬스터 데이터 리스트로 역직렬화하여 할당
                MonsterDataManager.instance.MonsterInventory = JsonConvert.DeserializeObject<PlayerMonsterData[]>(savedJsonData);
            }
        });

        // UserId에 있는 RuneInven 데이터를 데이터베이스에서 불러오기
        reference.Child(FireBaseAuthManager.Instance.UserId).Child("RuneInven").GetValueAsync().ContinueWith(task =>
        {
            if (task.IsFaulted)
            {
                // 예외 처리
                Debug.LogError("Error getting data: " + task.Exception);
                return;
            }
            if (task.IsCompleted)
            {
                // 데이터를 JSON 형식으로 변환
                DataSnapshot snapshot = task.Result;
                string jsonData = snapshot.GetRawJsonValue();
                // JSON 데이터를 파일에 저장
                string filePath = MonsterDataManager.instance.playerrunestoneDataPath;
                File.WriteAllText(filePath, jsonData);
                // 파일에서 JSON 데이터 읽기
                string savedJsonData = File.ReadAllText(filePath);

                MonsterDataManager.instance.RuneInventory = JsonConvert.DeserializeObject<RuneStone[]>(jsonData);
                // JSON 데이터를 몬스터 데이터 리스트로 역직렬화하여 할당
            }
        });
    }
```

</details>

***
