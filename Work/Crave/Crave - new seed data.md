  * Code
    * ```javascript
import fs from 'fs';
import { PrismaClient } from '@prisma/client';

import {
  TOOKAN_PROD_DOWNTOWN,
  TOOKAN_STAGING_DOWNTOWN,
  TOOKAN_PROD_MERIDIAN,
  TOOKAN_STAGING_MERIDIAN,
} from './facility';

const prisma = new PrismaClient();

const getTookanId = (id: string, isProduction: boolean) => {
  if (id === 'facility-downtown')
    return isProduction ? TOOKAN_PROD_DOWNTOWN : TOOKAN_STAGING_DOWNTOWN;

  return isProduction ? TOOKAN_PROD_MERIDIAN : TOOKAN_STAGING_MERIDIAN;
};

const createProductionFacilities = async () => {
  const facilities = await prisma.facility.findMany({});

  const json = {};

  for (const facility of facilities) {
    json[facility.id] = {
      ...facility,
      tookanTeamId: getTookanId(facility.id, false),
    };
  }

  fs.writeFileSync(
    './prisma/seeds-new/production-data/facilities.json',
    JSON.stringify(json),
  );

  return facilities;
};

const createProductionPromoBanners = async (facilityId: string) => {};

// promo banners
// workplaces and stations
// kitchens
// extras
// menu categories
// menu schedules
// overrides

const createProductionKitchens = async (facilityId: string) => {
  const kitchens = await prisma.kitchen.findMany({
    where: { facilityId },
    include: {},
  });

  const json = {};
};

const script = async () => {
  return true;
};

script()
  .then(() => process.exit(0))
  .catch((e) => {
    console.info(e);
    process.exit(1);
  });
```
  * Documentation
    * How to download production prisma client and download all current records?
