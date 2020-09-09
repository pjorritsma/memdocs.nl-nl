## <a name="enable-windows-10-automatic-enrollment"></a>Automatische inschrijving voor Windows 10 inschakelen

Met automatische inschrijving kunnen gebruikers hun Windows 10-apparaten inschrijven in Intune. Voor inschrijving voegen gebruikers hun werkaccount toe aan hun apparaten die persoonlijk eigendom zijn, of koppelen ze apparaten die bedrijfseigendom zijn aan Azure Active Directory. Het apparaat wordt op de achtergrond geregistreerd en aangesloten bij Azure Active Directory. Wanneer het apparaat is geregistreerd, wordt het met Intune beheerd.

**Vereisten**

- Azure Active Directory Premium-abonnement ([proefabonnement](https://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune-abonnement

### <a name="configure-automatic-mdm-enrollment"></a>Automatische MDM-registratie configureren

1. Meld u aan bij de [Azure-portal](https://portal.azure.com) en selecteer **Azure Active Directory**.

   ![Schermopname van de Azure-portal](../enrollment/media/windows-enroll/auto-enroll-azure-main.png)

2. Selecteer **Mobiliteit (MDM en MAM)** .

   ![Schermopname van de Azure-portal](../enrollment/media/windows-enroll/auto-enroll-mdm.png)

3. Selecteer **Microsoft Intune**.

   ![Schermopname van de Azure-portal](../enrollment/media/windows-enroll/auto-enroll-intune.png)

4. **Gebruikersbereik van MDM** configureren. Geef op van welke gebruikers apparaten moeten worden beheerd met Microsoft Intune. Deze Windows 10-apparaten kunnen automatisch worden ingeschreven voor beheer met Microsoft Intune.

   - **Geen** - Automatische inschrijving voor MDM uitgeschakeld
   - **Sommige** - Selecteer **Groepen** die automatisch hun Windows 10-apparaten kunnen inschrijven
   - **Alle** - Alle gebruikers kunnen automatisch hun Windows 10-apparaten inschrijven

      > [!IMPORTANT]
      > Voor Windows BYOD-apparaten krijgt het MAM-gebruikersbereik voorrang als zowel het MAM-gebruikersbereik als het MDM-gebruikersbereik (automatische MDM-registratie) zijn ingeschakeld voor alle gebruikers (of dezelfde groepen of gebruikers). Het apparaat wordt niet via MDM geregistreerd, en WIP-beleid (Windows Information Protection) wordt toegepast als u dit hebt geconfigureerd.
      >
      > Als u automatische inschrijving wilt inschakelen voor Windows BYOD-apparaten aan een MDM: configureer het MDM-gebruikersbereik op **Alle** (of **Een aantal**, en geef een groep op) en configureer het MAM-gebruikersbereik op **Geen** (of **Een aantal**, en geef een groep op - en zorg ervoor dat gebruikers geen lid zijn van een groep waarop zowel MDM- als MAM-gebruikersbereiken zijn gericht).
      >
      >Voor [zakelijke apparaten](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices) krijgt het MDM-gebruikersbereik voorrang als beide bereiken (MDM en MAM) zijn ingeschakeld. Het apparaat wordt automatisch ingeschreven bij het geconfigureerde MDM.

   > [!NOTE]
   > Het MDM-gebruikersbereik moet worden ingesteld op een Azure AD-groep die gebruikersobjecten bevat.

   ![Schermopname van de Azure-portal](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. Gebruik de standaardwaarden voor de volgende URL's:
    - **URL voor MDM-gebruiksvoorwaarden**
    - **Detectie-URL voor MDM**
    - **URL van MDM-naleving**

6. Selecteer **Opslaan**.

Tweeledige verificatie is standaard niet ingeschakeld voor de service. Tweeledige verificatie wordt echter aanbevolen bij het registreren van een apparaat. Om tweeledige verificatie in te schakelen, configureert u een provider voor tweeledige verificatie in Azure AD en configureert u uw gebruikersaccounts voor meervoudige verificatie. Zie [Aan de slag met de Azure Multi-Factor Authentication Server](/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).