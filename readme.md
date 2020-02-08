# github-release-script

Simple bash script to create a release on github.

## Sample Usage

    source logger.sh
    source github-releases-api.sh
    export GITHUB_OAUTH_TOKEN=***
    export GITHUB_BASE_URL=https://api.github.com/repos/adangel/github-releases-script
    
    git tag v1
    git push origin tag v1
    
    tagName="v1"
    targetCommitish="$(git rev-list -n 1 ${tagName})"
    gh_releases_createDraftRelease $tagName $targetCommitish
    GH_RELEASE="$RESULT"
    
    gh_release_updateRelease "$GH_RELEASE" "$tagName" "$tagName $(date -u +%d-%B-%Y)" "This is the first release."
    gh_release_uploadAsset "$GH_RELEASE" "github-releases-api.sh"
    gh_release_uploadAsset "$GH_RELEASE" "logger.sh"
    
    gh_releases_getLatestDraftRelease
    GH_RELEASE="$RESULT"
    gh_release_publishRelease "$GH_RELEASE"
