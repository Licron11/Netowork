#!/bin/bash

# Переменные
DEV_BRANCH="dev"
PRD_BRANCH="prd"
TAG_PREFIX="release-"

# Проверка, что скрипт выполняется в корневом каталоге репозитория
if [ ! -d .git ]; then
  echo "Этот скрипт должен выполняться в корневом каталоге Git-репозитория."
  exit 1
fi

# Обновление локальных веток
git fetch origin

# Переключение на ветку dev и обновление
git checkout $DEV_BRANCH
git pull origin $DEV_BRANCH

# Переключение на ветку prd и обновление
git checkout $PRD_BRANCH
git pull origin $PRD_BRANCH

# Слияние изменений из dev в prd
git merge $DEV_BRANCH

if [ $? -ne 0 ]; then
  echo "Произошла ошибка при слиянии. Пожалуйста, разрешите конфликты и повторите попытку."
  exit 1
fi

# Установка нового тега
NEW_TAG="${TAG_PREFIX}$(date +'%Y%m%d%H%M%S')"
git tag $NEW_TAG

# Отправка изменений и тега в удаленный репозиторий
git push origin $PRD_BRANCH
git push origin $NEW_TAG

echo "Изменения успешно перенесены из $DEV_BRANCH в $PRD_BRANCH и установлен тег $NEW_TAG."
