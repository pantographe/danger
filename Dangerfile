# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn("MR is classed as Work in Progress", sticky: true) if gitlab.mr_title.include? "WIP"

# Ensure that all MRs have an assignee.
warn("This MR does not have any assignees yet.", sticky: true) unless gitlab.mr_json["assignee"]

# Ensure there is a summary for a MR.
failure "Please provide a summary in the Merge Request description" if gitlab.mr_body.length < 20

# Note when MRs don't reference a milestone, make the warning stick around on subsequent runs
has_milestone = gitlab.mr_json["milestone"] != nil
warn("This MR does not refer to an existing milestone", sticky: true) unless has_milestone

# Note when a MR cannot be manually merged
can_merge = gitlab.mr_json["mergeable"]
warn("This MR cannot be merged yet.") unless can_merge

# Warn when there is a big %R
warn("Big MR") if git.lines_of_code > 500
