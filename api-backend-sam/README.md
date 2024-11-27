uniqueGridId=`date +%s`
baseUrl='https://zfxvdyr2fb.execute-api.ap-southeast-2.amazonaws.com/Prod/'

curl -X POST --data-binary @image01.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image02.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image03.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image04.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image05.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image06.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image07.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image08.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image09.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image10.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image11.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image12.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image13.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image14.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image15.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST --data-binary @image16.jpg "${baseUrl}addImage?uniqueGridId=${uniqueGridId}"

curl -X POST "${baseUrl}generateGrid?uniqueGridId=${uniqueGridId}"

Presigned_URL: https://sam-lab-destinationbucket-iy63xmoiv1pg.s3.amazonaws.com/3de3d657e110a9df89701f6f8d99a4fa.jpg?\#AWSAccessKeyId=\#ASIAUKCXU7J3TRCXQXVL&\#Signature=\#hNzLv89LGYIbQDSaNoEqrZ28UYA%3D&\#x-amz-security-token=\#IQoJb3JpZ2luX2VjEHEaCXVzLXdlc3QtMiJHMEUCIQDIaMRL3HqkvyXeg%2BqTS6cJ3vuHw2cezZa6hrJZncBzbAIgFWPz54E4Y9dGkgH3hzRtFi6TzW0NKvKQkTM9TWox9b8qpwMIGhAEGgwyOTY1MzY1NzA0ODciDLWScyKiPO6N66kYciqEAy94e3a6eoPKJxvCf9Mi%2By3i1cSu1IZ6GTvicjaUjSY2zrnWVUoeTwZJ31VhZUvdwqBl7difxlHUFRIgflbSvDuktCrTYBQ3TnT2bgm9GbOpFVc%2Bi6U%2BzCX4%2BAdqCwhki4oVPm7dKPsDabwyyGmZUm7z2WkYdHiUmvrFq1%2BHJJGSLlJ8LFu%2BgKTrvjaeO6tziw88XiDQeSolLu7wHqFb0nKRNMvvabRsWVvt91gEvU7EMeYw5%2FKTaA2O4uiDSQXq4%2BKbuHmPRj7RNgeb5EBWZKg%2BlTyN9L%2FBR2d7KccSeY%2BIItALxRvxLaQbPCkgZ236ZSnNWYX4Pr0UkWyBZSiGFG6MQxlBNCinhkJRDCo4Vh%2FWEh7VsWBwpXypiQk6DBI2eN28EnXbUU0Dq%2B7el47fFwqK1TbUvYXLj0Hm%2FTozUF50P5mU9mqcbmZ60uxwFEA5f%2Fuv6BPLWtZJTBEqDBq%2FK4GrBLOAMymCirtv1ZyiPb8p1RoNnGa2gO%2FnQr0pYvjDTs6cifgwts6SugY6nQHF%2B9wpAYP7nTHTQ9vWvR6aV05ueoMN5zWs%2Bwx6T8lMynFnG4t0rHZKaKWzmNhLumdUGCaNENIuJmRdeUKtFVFlsWcyeRe0Y3CPleVQi0aS2f57zbDLf6dS92Jq5RLMh%2FFj3lzwB9LAIg1BILQrlUPxtHuuopJUtqGEKQNfpfFLOKtkTvSbDTdg3zBDzU0WHmO74xunSwJa52BR6MLO&\#Expires=\#1732552806
