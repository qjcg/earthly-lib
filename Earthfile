VERSION --use-function-keyword 0.7

git-base:
    FROM caarlos0/svu:v1.12.0
    DO +GIT_CONFIG

GIT_CONFIG:
    FUNCTION
    ARG name = "Earthly CI"
    ARG email = "earthly.ci@example.com"
    RUN \
        git config --global user.name $name \
        && git config --global user.email $email

GIT_TAG:
    FUNCTION
    ARG tag = $(svu next)
    RUN git tag -am $tag $tag || echo Tag already exists: $tag

GIT_PUSH:
    FUNCTION
    ARG remote = origin
    ARG refs = main $(svu current)
    RUN git push --atomic $remote $refs

GIT_TAG_PUSH:
    FUNCTION
    DO +GIT_TAG
    DO +GIT_PUSH
