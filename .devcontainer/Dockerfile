# [Choice] .NET Core version: 3.1, 2.1
ARG VARIANT=6.0
FROM mcr.microsoft.com/vscode/devcontainers/dotnet:0-${VARIANT}

COPY Profile.ps1 /home/vscode/.config/powershell/Microsoft.PowerShell_profile.ps1
COPY library-scripts/azcli-debian.sh /tmp/library-scripts/
RUN bash /tmp/library-scripts/azcli-debian.sh \
    && curl -Lo /usr/local/bin/bicep https://github.com/Azure/bicep/releases/latest/download/bicep-linux-x64 \
    && chmod +x /usr/local/bin/bicep \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts \
    && git clone https://github.com/Azure/arm-ttk.git /usr/local/arm-ttk\
    && apt-get update \
    && apt-get install -y wget apt-transport-https software-properties-common \
    && wget -q https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb \
    && apt-get update \
    && sed -i "/^# deb.*universe/ s/^# //" /etc/apt/sources.list \
    && apt-get install -y powershell \
    && pwsh -c "Install-Module -Name PSRule -Scope AllUsers -Force" \
    && pwsh -c "Install-Module -Name PSRule.Rules.Azure -Scope AllUsers -Force" \
    && pwsh -c "Install-Module posh-git -Scope AllUsers -Force" \
    && pwsh -c "Install-Module oh-my-posh -Scope AllUsers -Force" \