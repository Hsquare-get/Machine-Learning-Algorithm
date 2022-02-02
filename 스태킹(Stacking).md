# 스태킹(Stacking)

여러 모델들의 예측값을 기반으로 **메타 모델이 재학습**하여 예측하는 기법

![Stacking](https://user-images.githubusercontent.com/64063767/152153691-7c9f6ab3-742b-42cc-b034-4bd6d25c9dc0.png)

예를 들어 KNN, Logistic Regression, RandomForest, XGBoost의 서로 다른 알고리즘을 활용해서 메타 모델(최종 모델)로 선정한 LightGBM을 재학습시킬 수 있다.

성능이 무조건 좋아지지 않기 때문에 현실 모델레서도 많이 사용되지는 않는다. 다만, 성능이 올라가는 경우가 더러 있기 때문에 캐글이나 데이콘 같은 미세한 성능차이로 승부를 결정하는 대회에서 주로 사용된다. 특히 기반 모델로 4개 이상을 선택해야 좋은 결과를 기대할 수 있다고 한다.

| 메타 모델의 학습 데이터                                      | 메타 모델의 테스트 데이터                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image](https://user-images.githubusercontent.com/64063767/152162397-74ed146d-b180-47c7-b291-ef8bf34c0bca.png) | ![image](https://user-images.githubusercontent.com/64063767/152162447-ce64bd0b-d747-4cc8-93fa-e15f2c382d4d.png) |

<br/>

## References

- [스태킹(Stacking) 완벽 정리](https://hwi-doc.tistory.com/entry/%EC%8A%A4%ED%83%9C%ED%82%B9Stacking-%EC%99%84%EB%B2%BD-%EC%A0%95%EB%A6%AC)